# 목차

## 기본적인 자료구조

- [자료구조란 무엇인가요](#자료구조란-무엇인가요)

  - 효율적으로 데이터를 관리해야 하는 이유 (예)

- [대표적인 자료구조는 어떤 것들이 있나요](#대표적인-자료구조는-어떤-것들이-있나요)

  - 선형 구조
  - 비 선형 구조

- [리스트](#리스트)
- [큐](#큐)
- [스택](#스택)
- [링크드 리스트](#링크드-리스트)
- [해쉬 테이블](#해쉬-테이블)
- [트리](#트리)
- [힙](#힙)
- [그래프](#그래프)

## 알고리즘에 활용되는 패턴과 자료구조

- [Frequency Counters](#Frequency-Counters)
- [Multiple Pointers](#Multiple-Pointers)
- [Sliding Window](#Sliding-Window)
- [Divide and conquer](#divide-and-conquer)
- [Recursion](#recursion)
- [Linear Search](#linear-search)
- [Naive String Search](#naive-string-search)
- [Binary Search](#binary-search)
- [Bubble Sort](#bubble-sort)
- [Selection Sort](#selection-sort)
- [Insertion Sort](#insertion-sort)
- [Merge Sort](#merge-sort)
- [Quick Sort](#quick-sort)
- [Single Linked List](#single-linked-list)
- [Dobule Linked List](#double-linked-list)
- [Stack](#stack)
- [Queue](#queue)
- [Binary Search Tree](#binary-search-tree)
- [Breadth First Search](#breadth-first-search)
- [Depth First Search](#depth-first-search)
- [Binary Heap](#binary-heap)
- [Priority Queue](#priority-queue)
- [Hash Table](#hash-table)
- [graph](#graph)
- [Dijkstra](#dijkstra)
- [Dynamic Programming](#dynamic-programming)

<br />

## 자료구조란 무엇인가요

자료구조란 대량의 데이터를 효율적으로 관리할 수 있는 데이터의 구조를 의미한다.

코드 상에서 효율적으로 데이터를 처리하기 위해, 데이터 특성에 따라, 체계적으로 데이터를 구조화 해야한다.

어떤 데이터 구조를 사용하느냐에 따라, 코드의 효율이 달라질 수 있다.

### 효율적으로 데이터를 관리해야 하는 이유 (예)

- 브라우저의 뒤로가기/앞으로가기의 경우 스택으로 구현
- 프린터 인쇄 대기열 구현의 경우 큐로 구현
- 파일 시스템 구조를 구현하기 위해 트리 구조를 활용
- 캐시 시스템을 구현하기 위해 해시 테이블을 활용
- 소셜 네트워크 친구 추천 시스템을 위해 그래프를 이용


<br />

## 대표적인 자료구조는 어떤 것들이 있나요

### 선형 구조

데이터들이 일렬로 쭉 저장되어 있는 형태

- 리스트
- 큐
- 스택
- 덱

### 비 선형 구조

데이터가 트리 형태로 저장되어 있다고 생각하고 사용하는 구조

- 트리
- 그래프
- 힙

<br />

## 리스트

- 데이터를 나열하고 각 데이터를 인덱스에 대응하도록 구성한 데이터 구조
- JS에서는 Array 타입이 배열 기능을 제공함

`리스트는 왜 필요한가요?`

- 같은 종류의 데이터를 효율적으로 관리하기 위해
- 같은 종류의 데이터를 순차적으로 저장하기 위해

`장점`

- 빠른 접근이 가능하다.
- 첫 데이터의 위치에서 상대적인 위치로 데이터에 접근이 가능하다.(인덱스 번호를 기반으로 접근이 가능하다.)

`단점`

- 데이터 추가/삭제가 어렵다
- 미리 최대 길이를 지정해야함(JS에서는 가변적으로 사용이 가능하다.)

`JS에서 리스트를 구현하는 방법`

```js
const list = [1, 2, 3, 4, 5];
const list = new Array(1, 2, 3, 4, 5);
const list = Array.from({ length: 5 }, (_, index) => index + 1);

// 배열 조작 메서드
const fruits = ['apple'];
fruits.push('banana');     // 끝에 추가
fruits.unshift('orange');  // 앞에 추가
fruits.pop();             // 끝에서 제거
fruits.shift();           // 앞에서 제거

// 주요 배열 메서드
const numbers = [1, 2, 3, 4, 5];

// map: 각 요소를 변환
const doubled = numbers.map(num => num * 2);  // [2,4,6,8,10]

// filter: 조건에 맞는 요소만 선택
const evenNumbers = numbers.filter(num => num % 2 === 0);  // [2,4]

// reduce: 누적 계산
const sum = numbers.reduce((acc, curr) => acc + curr, 0);  // 15

// find: 조건에 맞는 첫 요소 찾기
const firstEven = numbers.find(num => num % 2 === 0);  // 2

// some: 조건을 만족하는 요소가 있는지 확인
const hasEven = numbers.some(num => num % 2 === 0);  // true

// every: 모든 요소가 조건을 만족하는지 확인
const allEven = numbers.every(num => num % 2 === 0);  // false

```

<br />

## 큐

- 줄을 서는 행위와 유사
- 가장 먼저 넣은 데이터를 가장 먼저 꺼낼 수 있는 구조
- FIFO(First-In, First-Out) 또는 LILO(Last-In, Last-Out) 방식으로 스택과 꺼내는 순서가 반대

### 어디에 큐가 많이 쓰일까?

멀티 태스킹을 위한 프로세스 스케줄링 방식을 구현하기 위해 많이 사용된다.

```js
class Queue {
  // 큐 생성자
  // 큐는 비어있는 배열로 초기생성
  // 큐의 맨 앞과 맨 뒤를 가리키는 포인터를 0으로 초기화
  constructor() {
    this.items = [];
    this.front = 0;
    this.rear = 0;
  }

  // 큐에 요소 추가
  // 큐의 맨 뒤에 요소를 추가하고, 큐의 크기를 반환
  enqueue(element) {
    this.items[this.rear] = element;
    this.rear++;
    return this.items.length;
  }

  // 큐에서 요소 제거
  // 큐가 비었을 경우 null을 반환
  // 큐의 맨 앞에 있는 요소를 제거하고, 그 요소를 반환
  dequeue() {
    if (this.isEmpty()) {
      return null;
    }
    const item = this.items[this.front];
    delete this.items[this.front];
    this.front++;
    
    // 큐가 비었을 때 포인터 초기화
    if (this.front === this.rear) {
      this.front = 0;
      this.rear = 0;
    }
    
    return item;
  }

  // 맨 앞의 요소 확인
  // 큐가 비었을 경우 null을 반환
  // 큐의 맨 앞에 있는 요소를 반환
  peek() {
    if (this.isEmpty()) {
      return null;
    }
    return this.items[this.front];
  }

  // 큐가 비었는지 확인
  isEmpty() {
    return this.front === this.rear;
  }

  // 큐의 크기
  size() {
    return this.rear - this.front;
  }

  // 큐 초기화
  clear() {
    this.items = [];
    this.front = 0;
    this.rear = 0;
  }
}
```

다만 알고리즘을 풀때는 shift, push 메서드를 사용하는게 일반적인 것 같다.

## 스택

- 데이터를 제한적으로 접근할 수 있는 구조
- 한쪽 끝에서만 자료를 넣거나 뺄 수 있는 구조
- 가장 나중에 쌓은 데이터를 가장 먼저 빼낼 수 있는 데이터 구조

`스택 구조`

스택은 LIFO, 또는 FILO 데이터 관리 방식을 따른다.

`대표적인 스택의 활용`

컴퓨터 내부의 프로세스 구조의 함수 동작 방식

`주요 기능`

push(): 데이터를 스택에 넣기
pop(): 데이터를 스택에서 꺼내기

스택의 경우에는 JS에서 기본적으로 제공하는 배열을 통해서 구현이 가능하다.

## 링크드 리스트

Linked List 구조

- 연결 리스트라고도 한다.
- 배열은 순차적으로 연결된 공간에 데이터를 나열하는 데이터 구조
- 링크드 리스트는 떨어진 곳에 존재하는 데이터를 화살표로 연결해서 관리하는 데이터 구조

`링크드 리스트 기본 구조와 용어`

노드(Node) : 데이터 저장 단위(데이터값, 포인터)로 구성

포인터(pointer) : 각 노드 안에서, 다음이나 이전의 노드와 연결 정보를 가지고 있는 공간

일반적인 링크드 리스트 형태
```js
// 노드 클래스 정의
class Node {
  constructor(data) {
    this.data = data;    // 데이터를 저장
    this.next = null;    // 다음 노드를 가리키는 포인터, 노드를 저장한다. 정확히는 노드의 주소값이지만 객체 자체를 여기다가 할당한다고 생각하면 편하다.
  }
}

class LinkedList {
  constructor() {
    this.head = null;    // 첫 번째 노드를 가리키는 포인터
    this.size = 0;       // 리스트의 크기
  }

  // 맨 끝에 노드 추가
  append(data) {
    const newNode = new Node(data);

    if (!this.head) {
      this.head = newNode;
    } else {
      let current = this.head;
      // 마지막 노드를 반복문으로 찾는다.
      while (current.next) {
        current = current.next;
      }
      current.next = newNode;
    }
    // 추가가 끝났다면 리스트의 크기를 증가시킨다.
    this.size++;
  }

  // 특정 위치에 노드 삽입
  insert(data, position) {
    if (position < 0 || position > this.size) {
      return false;
    }

    const newNode = new Node(data);

    if (position === 0) {
      newNode.next = this.head;
      this.head = newNode;
    } else {
      let current = this.head;
      let previous = null;
      let index = 0;

      // 삽입할 위치의 이전 노드를 찾는다.
      while (index < position) {
        previous = current;
        current = current.next;
        index++;
      }

      // 삽입할 위치의 이전 노드와 새 노드를 연결한다.
      newNode.next = current;
      previous.next = newNode;
    }
    // 삽입이 끝났다면 리스트의 크기를 증가시킨다.
    this.size++;
    return true;
  }

  // 특정 위치의 노드 삭제
  removeAt(position) {
    if (position < 0 || position >= this.size) {
      return null;
    }

    let current = this.head;

    if (position === 0) {
      this.head = current.next;
    } else {
      let previous = null;
      let index = 0;

      // 삭제할 위치의 이전 노드를 찾는다.
      while (index < position) {
        previous = current;
        current = current.next;
        index++;
      }

      // 삭제할 위치의 이전 노드와 다음 노드를 연결한다.
      previous.next = current.next;
    }

    // 삭제가 끝났다면 리스트의 크기를 감소시킨다.
    this.size--;
    return current.data;
  }

  // 특정 데이터를 가진 노드 찾기
  indexOf(data) {
    let current = this.head;
    let index = 0;

    while (current) {
      if (current.data === data) {
        return index;
      }
      current = current.next;
      index++;
    }

    return -1;
  }

  // 리스트가 비어있는지 확인
  isEmpty() {
    return this.size === 0;
  }

  // 리스트의 크기 반환
  getSize() {
    return this.size;
  }

  // 리스트를 문자열로 변환
  toString() {
    let current = this.head;
    let string = '';

    while (current) {
      string += current.data + (current.next ? ' -> ' : '');
      current = current.next;
    }

    return string;
  }
}
```

장점

- 동적 크기 조정 가능
- 삽입 삭제가 효율적 O(1)
- 메모리를 효율적으로 사용

단점

- 임의 접근 불가(순차적 접근만 가능)
- 추가 메모리 필요(포인터 저장)
- 캐시 지역성이 낮음

### 더블 링크드 리스트

- 단방향 링크드 리스트의 경우 반드시 우리가 설정한 head의 차례로 데이터를 찾아갔다.
- 더블 링크드 리스트는 앞 뒤 방향 모두 노드 탐색이 가능하다.
- 이중 연결 리스트라고도 한다.
- 장점: 양방향으로 연결되어 있어서 노드 탐색이 양쪽 모두 가능하다.

```js
// 노드를 생성할 때 이전 노드를 참조하는 포인터를 추가한다.
// 이후 함수들에서도 이전 노드를 설정해주는 부분을 추가.
class Node {
  constructor(data) {
    this.data = data;    // 데이터
    this.prev = null;    // 이전 노드 참조
    this.next = null;    // 다음 노드 참조
  }
}

class DoublyLinkedList {
  constructor() {
    this.head = null;    // 첫 노드
    this.tail = null;    // 마지막 노드
    this.size = 0;       // 리스트 크기
  }

  // 맨 앞에 노드 추가
  prepend(data) {
    const newNode = new Node(data);

    if (this.isEmpty()) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      newNode.next = this.head;
      this.head.prev = newNode;
      this.head = newNode;
    }
    this.size++;
    return newNode;
  }

  // 맨 뒤에 노드 추가
  append(data) {
    const newNode = new Node(data);

    if (this.isEmpty()) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      newNode.prev = this.tail;
      this.tail.next = newNode;
      this.tail = newNode;
    }
    this.size++;
    return newNode;
  }

  // 특정 위치에 노드 삽입
  insert(data, position) {
    if (position < 0 || position > this.size) {
      return false;
    }

    if (position === 0) {
      return this.prepend(data);
    }

    if (position === this.size) {
      return this.append(data);
    }

    const newNode = new Node(data);
    let current = this.head;
    let index = 0;

    while (index < position) {
      current = current.next;
      index++;
    }

    newNode.prev = current.prev;
    newNode.next = current;
    current.prev.next = newNode;
    current.prev = newNode;
    
    this.size++;
    return newNode;
  }

  // 특정 위치의 노드 삭제
  removeAt(position) {
    if (position < 0 || position >= this.size) {
      return null;
    }

    let current = this.head;

    if (position === 0) {
      this.head = current.next;
      if (this.head) {
        this.head.prev = null;
      } else {
        this.tail = null;
      }
    } else if (position === this.size - 1) {
      current = this.tail;
      this.tail = current.prev;
      this.tail.next = null;
    } else {
      let index = 0;
      while (index < position) {
        current = current.next;
        index++;
      }
      current.prev.next = current.next;
      current.next.prev = current.prev;
    }

    this.size--;
    return current.data;
  }

  // 특정 데이터를 가진 노드 찾기
  find(data) {
    let current = this.head;
    let index = 0;

    while (current) {
      if (current.data === data) {
        return { node: current, index };
      }
      current = current.next;
      index++;
    }

    return null;
  }

  // 앞에서부터 순회
  forwardTraverse() {
    let current = this.head;
    const result = [];
    
    while (current) {
      result.push(current.data);
      current = current.next;
    }
    
    return result;
  }

  // 뒤에서부터 순회
  backwardTraverse() {
    let current = this.tail;
    const result = [];
    
    while (current) {
      result.push(current.data);
      current = current.prev;
    }
    
    return result;
  }

  // 리스트가 비어있는지 확인
  isEmpty() {
    return this.size === 0;
  }

  // 리스트 크기 반환
  getSize() {
    return this.size;
  }

  // 리스트 초기화
  clear() {
    this.head = null;
    this.tail = null;
    this.size = 0;
  }
}
```

## 해쉬 테이블

키에 데이터를 저장하는 데이터 구조

- 키를 통해 바로 데이터를 받아올 수 있으므로, 속도가 획기적으로 빨라진다
- 자바스크립트에서는 Object, Map 타입이 해쉬 테이블의 기능을 제공한다.
- 보통 배열로 미리 Hash Table 사이즈만큼 생성 후에 사용

- 해쉬(Hash): 임의 값을 고정 길이로 변환하는 것
- 해쉬 테이블(Hash Table): 키 값의 연산에 의해 직접 접근이 가능한 데이터 구조
- 해싱 함수(Hashing Function): Key를 해싱 함수로 연산해서, 해쉬 값을 알아내고, 이를 기반으로 해쉬 테이블에서 해당 Key에 대한 데이터 위치를 일관성있게 찾을 수 있음
- 슬롯(Slot): 한 개의 데이터를 저장할 수 있는 공간
- 저장할 데이터에 대해 Key를 추출할 수 있는 별도 함수도 존재할 수 있음

- 주요 용도

  - 검색이 많이 필료한경우
  - 저장, 삭제, 읽기가 빈번한 경우
  - 캐쉬 구현시
  - 캐쉬는 동일한 페이지를 불러오는 경우 변경되는 데이터 이외에는 사용자의 캐쉬 메모리에 저장하여 서버로 부터 불러오는 데이터의 양을 관리하기 위한 메모리이다.

- JS에서는 Object, Map 타입이 기능을 제공하지만 대부분 해쉬테이블이 필요한 경우에는 Map을 사용하는게 효과적



## 트리

`트리(Tree) 구조`

- 트리: 노드와 브랜치를 이용해서 사이클을 이루지 않도록 구성한 데이터 구조

- 트리구조에서 Siblings 끼리는 브랜치로 이어지지 않는다

`실제 사용 예시`

- 트리 중 이진 트리 형태의 구조로, 탐색 알고리즘 구현을 위해 많이 사용됨
- 트리 내부에 어떤 값을 가진 데이터가 존재하는지의 유무를 파악하기 쉽다.
- 배열을 통해 배열의 길이만큼 전부 순회하는 것 보다 기준(left, right)를 가지고 탐색하므로 더욱 빠르다

#### 용어

- Node: 트리에서 데이터를 저장하는 기본요소
- Root Node: 트리 맨 위(최 상단)에 있는 노드
- Level: 최상위 노드를 Level 0으로 하였을 때, 하위 Branch로 연결된 노드의 깊이를 나타냄
- Parent Node: 어떤 노드의 다음 레벨에 연결된 노드
- Child Node: 어떤 노드의 상위 레벨에 연결된 노드
- Leaf Node (Terminal Node): Child Node가 하나도 없는 노드
- Sibling (Brother Node): 동일한 Parent Node를 가진 노드
- Depth: 트리에서 Node가 가질 수 있는 최대 Level (깊이를 나타냄)

#### 이진 트리와 이진 탐색트리

- 이진트리: 노드와 최대 브랜치가 2개인 트리
  - 이진 트리 구조에서 워낙 이진 탐색 트리 형식으로 많이 쓰기 때문에 이진트리 = 이진탐색트리라고 생각하는 경우가 있지만 둘은 같지 않다.
  - 이진트리는 루트 노드의 최대 브랜치가 2개인 트리이며, 사이클을 이루지 않도록 구성한 데이터구조이지만, 이진 탐색 트리는 해당 이진 트리의 특징을 바탕으로 특정 조건을 붙인 트리이다.

- 이진 탐색 트리: 이진 트리에 다음과 같은 추가적인 조건이 있는 트리
  - 왼쪽노드는 해당 노드보다 작은 값, 오른쪽 노드는 해당 노드보다 큰 값을 가지고 있음

#### 자료 구조 이진 탐색 트리의 장점과 주요 용도

- 주요 용도: 데이터 검색(탐색)
- 장점: 탐색 속도를 개선할 수 있음


### 이진트리 JS
```js
// 노드 클래스
class Node {
    constructor(value) {
        this.value = value;
        this.left = null;
        this.right = null;
    }
}

class BinaryTree {
    constructor() {
        this.root = null;
    }

    // 전위 순회 (Root -> Left -> Right)
    preOrder(node = this.root) {
        if (node === null) return [];
        
        return [
            node.value,
            ...this.preOrder(node.left),
            ...this.preOrder(node.right)
        ];
    }

    // 중위 순회 (Left -> Root -> Right)
    inOrder(node = this.root) {
        if (node === null) return [];
        
        return [
            ...this.inOrder(node.left),
            node.value,
            ...this.inOrder(node.right)
        ];
    }

    // 후위 순회 (Left -> Right -> Root)
    postOrder(node = this.root) {
        if (node === null) return [];
        
        return [
            ...this.postOrder(node.left),
            ...this.postOrder(node.right),
            node.value
        ];
    }

    // 레벨 순회 (너비 우선 탐색)
    levelOrder() {
        if (!this.root) return [];

        const result = [];
        const queue = [this.root];

        while (queue.length > 0) {
            const node = queue.shift();
            result.push(node.value);

            if (node.left) queue.push(node.left);
            if (node.right) queue.push(node.right);
        }

        return result;
    }
}

```

### 이진탐색트리 JS

```js
class BinarySearchTree {
    constructor() {
        this.root = null;
    }

    // 노드 삽입
    insert(value) {
        const newNode = new Node(value);

        if (this.root === null) {
            this.root = newNode;
            return this;
        }

        let current = this.root;
        while (true) {
            if (value === current.value) return undefined;
            
            if (value < current.value) {
                if (current.left === null) {
                    current.left = newNode;
                    return this;
                }
                current = current.left;
            } else {
                if (current.right === null) {
                    current.right = newNode;
                    return this;
                }
                current = current.right;
            }
        }
    }

    // 값 검색
    find(value) {
        if (!this.root) return false;

        let current = this.root;
        while (current) {
            if (value === current.value) return true;
            if (value < current.value) {
                current = current.left;
            } else {
                current = current.right;
            }
        }
        return false;
    }

    // 최소값 찾기
    findMin() {
        if (!this.root) return null;

        let current = this.root;
        while (current.left) {
            current = current.left;
        }
        return current.value;
    }

    // 최대값 찾기
    findMax() {
        if (!this.root) return null;

        let current = this.root;
        while (current.right) {
            current = current.right;
        }
        return current.value;
    }

    // 노드 삭제
    remove(value) {
        this.root = this._removeNode(this.root, value);
    }

    _removeNode(node, value) {
        if (node === null) return null;

        if (value < node.value) {
            node.left = this._removeNode(node.left, value);
            return node;
        } else if (value > node.value) {
            node.right = this._removeNode(node.right, value);
            return node;
        } else {
            // 삭제할 노드를 찾은 경우

            // Case 1: 리프 노드
            if (node.left === null && node.right === null) {
                return null;
            }

            // Case 2: 하나의 자식만 있는 경우
            if (node.left === null) return node.right;
            if (node.right === null) return node.left;

            // Case 3: 두 자식이 모두 있는 경우
            let minRight = this._findMin(node.right);
            node.value = minRight.value;
            node.right = this._removeNode(node.right, minRight.value);
            return node;
        }
    }

    _findMin(node) {
        while (node.left) {
            node = node.left;
        }
        return node;
    }
}

// 사용 예제
const bst = new BinarySearchTree();

// 삽입
bst.insert(10);
bst.insert(5);
bst.insert(15);
bst.insert(2);
bst.insert(7);

// 검색
console.log(bst.find(7));  // true
console.log(bst.find(9));  // false

// 최소/최대값
console.log(bst.findMin());  // 2
console.log(bst.findMax());  // 15

// 순회
console.log(bst.inOrder());  // [2, 5, 7, 10, 15]
```

## 힙

### 힙(Heap) 이란?

- 자료 구조의 힙: 데이터에서 최대값과 최소값을 빠르게 찾기 위해 고안된 완전 이진 트리(Complete Binary Tree)
- 완전 이진 트리 : 노드를 삽입할 때 최 하단의 왼쪽 노드부터 차례대로 삽입하는 트리
- 트리를 기반으로 한 변형된 정책을 쓰고 있다고 생각하면 됨
- js의 실행 컨텍스트에서 객체를 담아두는 공간인 Heap 메모리와 자료구조에서 Heap은 다르다.

### 메모리 힙

프로그램이 실행되면 4개의 메모리 영역을 가지게 된다.

이 중 Heap 영역은 사용자가 동적 할당을 할 경우 메모리에 저장된다.

### 자료구조의 힙

힙은 완전 이진트리. 최소 값 혹은 최대 값을 찾아내는연산에 적합하다.

힙에는 최소 힙과 최대 힙이 있다. 최대 힙은 루트노드로 갈수록 값이 커지며, 최소 힙은 루트 노드로 갈수록 값이 작아진다.

- 힙을 사용하는 이유

  - 배열에 데이터를 넣고, 최대값과 최소값을 찾으려면 O(n)이 걸린다 (전체를 순회해야 하기 때문)
  - 이에 반해, 힙에 데이터를 넣고, 최대값과 최소값을 찾으면 $ O(log n) $ 이 걸림
  - 우선 순위 큐와 같이 최대값 또는 최소값을 빠르게 찾아야 하는 자료구조 및 알고리즘 구현 등에 활용됨

### 힙 구조

- 힙은 최대값을 구하기 위한 구조와 최소값을 구하기 위한 구조로 분류할 수 있다.
1. 각 노드의 값은 해당 노드의 자식 노드가 가진 값보다 크거나 같다.
2. 완전 이진 트리 형태를 가진다.

```js
class MinHeap {
    // 힙 초기화
    constructor() {
        this.heap = [];  // 배열로 힙을 구현
    }

    // 부모 노드의 인덱스 반환
    getParentIndex(index) {
        return Math.floor((index - 1) / 2);
        // 예: index가 3일 때, (3-1)/2 = 1 -> 1번 인덱스가 부모
    }

    // 왼쪽 자식 노드의 인덱스 반환
    getLeftChildIndex(index) {
        return 2 * index + 1;
        // 예: index가 1일 때, 2*1+1 = 3 -> 3번 인덱스가 왼쪽 자식
    }

    // 오른쪽 자식 노드의 인덱스 반환
    getRightChildIndex(index) {
        return 2 * index + 2;
        // 예: index가 1일 때, 2*1+2 = 4 -> 4번 인덱스가 오른쪽 자식
    }

    // 두 노드의 위치를 교환
    swap(index1, index2) {
        const temp = this.heap[index1];
        this.heap[index1] = this.heap[index2];
        this.heap[index2] = temp;
    }

    // 새로운 값을 힙에 추가
    push(value) {
        this.heap.push(value);  // 배열 끝에 새 값 추가
        this.heapifyUp(this.heap.length - 1);  // 힙 속성 유지를 위해 위로 이동
    }

    // 삽입 후 힙 속성 유지 (상향식)
    heapifyUp(index) {
        while (index > 0) {  // 루트에 도달할 때까지
            const parentIndex = this.getParentIndex(index);
            // 부모가 현재 노드보다 작거나 같으면 중단
            if (this.heap[parentIndex] <= this.heap[index]) break;
            // 그렇지 않으면 부모와 위치 교환
            this.swap(index, parentIndex);
            index = parentIndex;
        }
    }

    // 최소값(루트)을 제거하고 반환
    pop() {
        if (this.heap.length === 0) return 0;
        if (this.heap.length === 1) return this.heap.pop();

        const min = this.heap[0];  // 최소값 저장
        this.heap[0] = this.heap.pop();  // 마지막 노드를 루트로 이동
        this.heapifyDown(0);  // 힙 속성 유지를 위해 아래로 이동

        return min;
    }

    // 삭제 후 힙 속성 유지 (하향식)
    heapifyDown(index) {
        const length = this.heap.length;
        let smallest = index;

        while (true) {
            const leftIndex = this.getLeftChildIndex(index);
            const rightIndex = this.getRightChildIndex(index);

            // 왼쪽 자식이 더 작으면 교환 대상을 왼쪽으로
            if (leftIndex < length && this.heap[leftIndex] < this.heap[smallest]) {
                smallest = leftIndex;
            }

            // 오른쪽 자식이 더 작으면 교환 대상을 오른쪽으로
            if (rightIndex < length && this.heap[rightIndex] < this.heap[smallest]) {
                smallest = rightIndex;
            }

            // 교환이 필요 없으면 중단
            if (smallest === index) break;

            // 현재 노드와 가장 작은 자식을 교환
            this.swap(index, smallest);
            index = smallest;
        }
    }
}
```

## 그래프

그래프는 실제 세계의 현상이나 사물을 정점 또는 노드와 간선으로 표현하기 위해 사용한다.

집에서 회사로 가는 경로를 그래프로 표현할 수 도 있다.

### 그래프 관련 용어

노드 : 정점 : 위치를 말한다

간선 = 링크 = 브랜치 : 위치 간의 관계를 표시한 선으로 노드를 연결한 선이라고 보면 됨

인접 정접 : 간선으로 직접 연결된 정점 (또는 노드)

