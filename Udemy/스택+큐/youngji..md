Stack
=============
선형 자료구조의 일종으로 Last In First Out(LIFO). 즉, 나중에 들어간 원소가 먼저 나온다. 이것은 Stack 의 가장 큰 특징이다. 차곡차곡 쌓이는 구조로 먼저 Stack에 들어가게 된 원소는 바닥에 깔리게 된다. 그렇게 때문에 늦게 들어간 녀석들은 그 위에 쌓이게 되고 호출 시 가장 위에 있는 녀석이 호출되는 구조이다.

### where stacks are used
- Managing function invacation
- Undo/ Redo
- Routing (the history object) is trated lick a stack!

### 배열로 **stack** 구현
```JS
let stack = [];
stack.push('google') //['google']
stack.push("instagram") // ["google", "instagram"]
stack.pop() // 'instagram'
stack.pop() // 'google'
// => 배열의 끝에 추가하고 배열의 끝에서 제거


stack.unshift("create new file") // ["create new file"]
stack.unshift("resized file") // ["resized file", "create new file"]
stack.shift() // "resized file"
stack.shift() // "create new file"
// 배열의 앞에 추가하고 앞에서 제거   
// 앞에 추가하면 새로운 인덱스를 부여해야함
// => 빅오표기법과 시간 복잡도에 따르면 좋지않음!!
```
## 스크래치로 스택 작성  
```JS
class Node {
    constructor(value){
        this.value= value;
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
        // create new node with the value
        var newNode = new Node(val);
        if(!this.first){
            // if there are no nodes in the stack, set the first and last property to be the newly created node
            this.first = newNode;
            this.last = newNode;
        } else {
            // If there is at least one node, create a variable that stores the current fist propoerty on the stack
            var temp = this.first;
            this.first = newNode;
            this.first.next = temp;
        }
        // increment the size of the stack by 1
        return ++this.size;
    }
    // (2) pop
}

var stack = new Stack();
stack.push(23);
stack.push(230);
stack.push(2301);
// {first: Node{value: 2301, next: Node},
// last: Node{value:23, next: null},
// size: 3}

```
### (2) pop 만들기
```JS
pop(){
    if(!this.first) return null;
    var temp = this.first;
    if(this.first === this.last){
        this.last = null;
    }
    this.first = this.first.next;
        this.size--;
        return temp.value;
}

```

<br />

Stack
=============
선형 자료구조의 일종으로 First In First Out(FIFO). 즉, 먼저 들어간 놈이 먼저 나온다. Stack과는 반대로 먼저 들어간 놈이 맨 앞에서 대기하고 있다가 먼저 나오는 구조이다.

### 배열로 **queue** 구현
```JS
var q = [];
q.push("FIRST");
q.push("SECOND");
q.push("THIRD");
// ["FIRST", "SECOND", "THIRD"];

q.shift() // "FIRST"
q.shift() // "SECOND"
q.shift() // "THIRD"
//=> 다시 인덱스 부여해야하므로 별로 안좋음!!

q.unshift("FIRST");
q.unshift("SECOND");
q.unshift("THIRD");
// ["THIRD", "SECOND", "FIRST"]

q.pop() // "FIRST"
q.pop() // "SECOND"
q.pop() // "THIRD"
```

## 스크래치로 스택 작성  
```JS
class Node {
    constructor(value){
        this.value = value;
        this.next = null;
    }
}

class Queue {
    constructor(){
        this.first = null;
        this.last = null;
        this.size = 0;
    }
    enqueue(val){
        var newNode = new Node(val);
        if(!this.first){
            this.first = newNode;
            this.last = newNode;
        } else {
            this.last.next = newNode;
            this.last = newNode;
        }
        return ++this.size;
    }

    dequeue(){
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