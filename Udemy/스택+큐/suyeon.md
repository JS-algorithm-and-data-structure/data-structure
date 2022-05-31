# 스택(Stack)
## 1. 스택(Stack) 소개
> **LIFO: Last In First Out**
스택은 후입선출 원칙을 따르는 자료구조
### WHERE: 어디에서 사용되는가
- 함수 호출
- 실행 취소 / 다시 실행(Undo / Redo)
- 인터넷 브라우저 방문 기록
## 2. 배열로 스택 만들기
### 1. push / pop: 뒤에서 넣고 뒤에서 빼기
```
var stack = []
stack.push(‘google’)
stack.push(‘instagram’)
stack.push(‘youtube’)
stack.pop() // youtube
stack.pop() // instagram
```
### 2. unshift / shift: 앞에서 넣고 앞에서 빼기
```
var stack = []
stack.unshift(‘create new file’)
stack.unshift(‘resized file’)
stack.unshift(‘cloned out wrinkle’)
stack.shift() // cloned out wrinkle
stack.shift() // resized file
```
## 3. 단일 연결 리스트로 자신만의 스택 작성하기
> push / pop은 상수 시간을 가져야하므로 unshift / shift를 이용해 만든다.
### push
- 값 하나를 입력받아 새로운 노드를 만든다.
- 스택에 노드가 없으면 새로운 노드가 first이자 last가 되도록 설정
- 노드가 하나라도 있으면 현재 first를 저장하는 변수를 만들고 first가 새로운 노드가 되도록 설정
- 노드의 next 프로퍼티가 아까 만들어둔 변수가 되도록 하고 size 1을 키운다.
### pop
- 스택에 노드가 없다면 null을 반환
- 비어있지 않다면 first 프로퍼티를 취해 변수에 저장 후 가장 마지막에 출력
- 만약 노드가 하나뿐이라면(first와 last가 같으면) first와 last프로퍼티를 null로 설정
- 노드가 하나 이상이면 first 프로퍼티를 다음 first 요소의 next로 설정하고(다음 요소를 앞으로 가져오기) size를 1 줄인 후 제거된 노드의 값 출력
```
class Node {
    constructor(value){
        this.value = value;
        this.next = null;
    }
}
class Stack {
    constructor(){
        this.first = null;
        this.last = null;
        this.size = 0;
    }
    push(val){
        var newNode = new Node(val);
        if (!this.first) {
            this.first = newNode;
            this.last = newNode;
        }else{
            var temp = this.first;
            this.first = newNode;
            this.first.next = temp;
        }
        return ++this.size;
    }
    pop(){
        if(!this.first) return null;
        var temp = this.first;
        if(this.first === this.last) {
            this.last = null;
        }
        this.first = this.first.next;
        this.size--;
        return temp.value;
    }
}
```
## 4. 스택의 빅오 (BIG O)
- 삽입 Insertion - O(1)
- 제거 Removal - O(1)
- 탐색 Searching - O(N)
- 접근 Access - O(N)
스택은 삽입, 제거를 우선시한다. 탐색, 접근을 우선시할 경우 다른 자료구조 사용 권장
***
# 큐(Queue)
## 5. 큐(Queue) 소개
> **FIFO: First In First Out**
큐는 선입선출 원칙을 따르는 자료구조
### WHERE: 어디에서 사용되는가
- 백그라운드 작업
- 파일 업로드
- 프린트 대기열
## 6. 배열을 사용해 큐 만들기
### 1. push / shift
```
var q = [];
q.push(‘first’)
q.push(‘second’)
q.push(‘third’)
console.log(q) // [‘first’,‘second’,‘third’]
q.shift() // first
q.shift() // second
q.shift() // third
console.log(q) // []
```
### 2. unshift / pop
```
var q = [];
q.unshift(‘first’)
q.unshift(‘second’)
q.unshift(‘third’)
console.log(q) // [‘third’,‘second’,‘first’]
q.pop() // first
q.pop() // second
q.pop() // third
console.log(q) // []
```
## 7. 스크래치로 자신만의 큐 작성하기
### Enqueue
- 값을 하나 입력 받는다
- 입력된 값을 가지고 노드를 새로 만든다.
- 큐 안에 노드가 없다면 새로운 노드를 first, last 프로퍼티로 설정한다.
- 노드가 있다면 현재 last의 next 프로퍼티가 새로운 노드가 되도록 하고 last 포인터를 맨 끝에 있는 새로운 노드로 옮긴다.
### Dequeue
- 인수를 입력하지 않는 함수를 정의한다.
- 만약 first 프로퍼티가 없으면 null 출력
- first 프로퍼티는 변수에 저장
- 리스트에 하나의 요소만 남아있다면 last를 null로 설정
- this.first를 사용해 그 다음 요소로 바꾼다.
- size를 1 줄이고 노드의 값 출력
```
class Node {
    constructor(value){
        this.value = value;
        this.next = null
    }
}
class Queue {
    constructor(){
        this.first = null;
        this.last
    }
    enqueue(val){
        var newNode = new Node(val);
        if(!this.first){
            this.first = newNode;
            this.last = newNode;
        } else {
            this.last.next = newNode;
            this.last = newNode
        }
        return ++this.size;
    }
    dequeue(){
        if(!this.first) return null;
        var temp = this.first;
        if(this.first === this.last){
            this.last = null;
        }
        this.first = this.first.next;
        this.size--;
        return temp.value;
    }
}
```
## 8. 큐의 빅오 (BIG O)
- 삽입 Insertion - O(1)
- 제거 Removal - O(1)
- 탐색 Searching - O(N)
- 접근 Access - O(N)