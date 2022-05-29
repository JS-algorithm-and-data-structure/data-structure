## Stack이란?
- 선입선출, LIFO (Last In, First Out)
- history object로 뒤로가기를 실행하는 것이나 cmd + z 로 마지막 행동을 취소하는 것도 스택의 가장 위에 있는 것을 제거하는 것이 된다.

## 내장 배열로 스택만들기

### push & pop
```
var stack = [];

stack.push("google");
stack.push("instagram");
stack.push("youtube");

consol.log(stack); //[ 'google', 'instagram', 'youtube' ]

stack.pop(); //'youtube'
stack.pop(); // 'instagram'

stack.push("amazon");
stack.pop(); // 'amazon'
```

### unshift & shift
```
var stack = [];

stack.unshift("create new file");
stack.unshift("resized file");
stack.unshift("cloned out wrinkle");

consol.log(stack); // [ 'cloned out wrinkle', 'resized file', 'create new file' ]

stack.shift(); //'cloned out wrinkle'
stack.shift(); //'resized file'
stack.shift(); //'create new file'

console.log(stack); // []

```
- 하지만 효율성을 생각했을때 (특히 데이터가 큰 경우)후입선출만 지키면 된다면 (인덱스를 사용해서 접근해야 하는 것이 아니라면)배열을 스택으로 이용하는 것보다 **연결 리스트**를 사용하는 것이 낫다.
- 일반적으로 배열을 사용할 때는 인덱스를 하나씩 shift하지 않아도 되는 **push & pop**을 이용하는 것이 낫다.

## 단일 연결 리스트로 stack 만들기
- 연결 리스트로 stack을 사용할 때는 리스트의 끝까지 가지 않아도 되는 **unshift & shift**를 이용하는 것이 효율적이다.
### push 만드는 순서
- push 함수는 입력받은 값으로 새로운 노드 하나를 만든다.
- 노드가 하나라도 있을 경우 현재 first를 저장하는 임시변수를 만든다.
- 새로운 노드가 first가 되도록 설정한다.
- 그리고 노드들을 모두 연결한다.
- next 노드가 먼저 먼저 생성된 노드를 가진 변수가 되도록 한다.
- size를 1 늘려준다.

### pop 만드는 순서
- stack에 노드가 없다면 null 반환
- 있다면 first노드를 임시변수에 저장한다.
- 만약 노드가 하나라면 first와 last 프로퍼티를 전부 null로 설정한다.
- 노드가 하나 이상이라면 first 프로퍼티를 다음 first 요소의 next로 설정한다.
- size를 1 줄인 후 제거된 노드의 값을 출력한다.

```
class Node {
 constructor (value) {
   this.value = value;
   this.next = null;
 } 
}


class Stack {
  constructor () {
    this.first = null;
    this.last = null;
    this.size = 0;
  }
  
  // 이름은 push 이지만 unshift의 역할
  push(val) {
    var newNode = new Node(val); // 새로 추가된 요소
    if (!this.first) { // 노드가 하나도 없을 경우
      this.first = newNode;
      this.last = newNode;
    } else {
      var temp = this.first; // 임시로 먼저 생성된 노드 저장
      this.first = newNode; // 새로운 노드가 first가 되게 설정
      this.first.next = temp; // 먼저 생성된 노드가 새로운 first의 다음 요소가 되게 설정
    }
    return ++this.size; // size 증가
  }

  // 이름은 pop이지만 shift의 역할
  pop(val) {
    if(!this.first) return null; // 제거할 노드가 없는 경우
    var temp = this.first; // 임시변수에 앞선 노드를 저장
    if(this.first === this.last) { // edge case: 노드가 하나만 있는 경우
      this.last = null;
    }
    this.first = this.first.next; //next 노드를 first로 설정
    this.size--;
    return temp.value;
  }
  }
}
```
### 결과
```
var stack = new Stack();
stack.push("FIRST");
stack.push("SECOND");
stack.push("THIRD");

console.log(stack);
// ======== stack =========
Stack {
  first: Node {
    value: 'THIRD',
    next: Node {
      value: 'SECOND',
      next: Node { value: 'FIRST', next: null },
      __proto__: { constructor: ƒ Node() }
    }
  },
  last: Node { value: 'FIRST', next: null },
  size: 3,
  ['__proto__']: {constructor: ƒ Stack(), push: ƒ push() }
}
// =======================

stack.pop(); //'THIRD'
stack.pop(); //'SECOND'
stack.pop(); //'FIRST'
stack.pup(); // null

```

## Stack의 Big O
- 삽입: O(1)
- 제거: O(1)
- 검색: O(N)
- 접근: O(N)