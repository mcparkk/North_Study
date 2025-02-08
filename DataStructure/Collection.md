
### 자료구조
자료구조(Data Structure) 일련의 일정 타입들의 데이터 모임 또는 관계를 나타낸 구성체이다.

흔히 사용되는 방법은 선형 자료구조(Linear Data Structure)와 비선형 자료구조로 나눌 수 있다.

**선형 자료구조(Linear Data Structure)** : 자료 간의 앞뒤 관계가 **1:1**, 일렬로 연결된 형태이며 대표적으로 **리스트(List), 큐(Queue), 덱(Deque)** 이 있다.

**비선형 자료구조(Nonlinear Data Structure)** : 하나의 자료 뒤에 여러개의 자료가 존재할 수 있는 **1:n**, 또는 **n:n**의 관계이며 대표적으로 **그래프(Graph), 트리(Tree)** 가 있다.

두 가지 분류에 해당되지 않는 자료구조  **집합(Set)** 은 보통 기타 자료구조 또는 집합 자료구조로 분류된다.

## Java Collections FrameWork
---
컬렉션(collection)이란 많은 수의 데이터를 그 **사용 목적에 적합한 자료구조로 묶어 하나로 그룹화**한 객체를 말한다. 즉, 데이터를 저장하는 구조와 데이터를 처리하는 알고리즘을 구조화하여 클래스로 구현해 놓은 것을 말한다.

자바에서 제공하는 Collection은 크게 3가지 Interface로 나눠눠져있다. 크게 리스트(List), 큐(Queue), 집합(Set)으로 나뉘어 있다.
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdxksJ0%2Fbtr2sFfD80G%2FhPz44mC48qtM4KPgfKh1T1%2Fimg.png">

### List 인터페이스
---
대표적인 선형 자료구조로 **순서**가 있는 데이터를 **목록으로** 이용할 수 있도록 만들어진 인터페이스이다.
중복되는 데이터들을 저장해야 할 때, 배열에 들어간 순서를 유지하고 싶을 때 사용된다.

List 인터페이스의 Collection의 다른 인터페이스들과 가장 큰 차이는 **배열처럼 순서가 있다는 것**이다.

<List Interface에 선언된 대표적인 메소드>
<img src="
https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FefYO5c%2FbtqI07cgkG0%2F9kd7yxy8aMkk2c40FWbPZ1%2Fimg.png">

#### ArrayList
* **배열**을 이용하여 만든 리스트이다.
* 데이터의 저장 **순서가 유지**되고 **중복을 허용**한다.
* 단방향 포인터 구조로 각 데이터에 대한 인덱스를 가지고 있어 **조회** 기능의 성능이 **빠르다**.

* 순차적으로 삽입/삭제 하는 경우에는 가장 빠르다.
* 리스트 중간의 데이터 삽입/삭제 시 나머지 노드의 위치를 조정해야 하기 때문에 느리다.
  a(값, 순서)

```
List<T> arrayList = new ArrayList<>();
```

#### LinkedList
- **노드(객체)를 연결**하여 리스트 처럼 만든 리스트이다.
- 노드는 **데이터**를 저장하는 부분과 다음 노드에 대한 **포인터**로 이루어져있다.
    - 이때 첫번째 노드를 헤드(Head), 마지막 노드를 테일(Tail)이라고 부른다.

- 리스트의 삽입/삭제 시 주소 값만 변경해주면 되기 때문에 ArrayList보다 효율적이다.
- 조회 시 첫 노드부터 순회하기 때문에 탐색 속도가 느리다.

<img src="https://velog.velcdn.com/images%2Fwoojinn8%2Fpost%2Ff384a51f-73cb-4e99-82c0-5643470d7585%2F%EB%A7%81%ED%81%AC%EB%93%9C%EB%A6%AC%EC%8A%A4%ED%8A%B8%EA%B5%AC%EC%A1%B0.PNG">

```
LinkedList<타입> linkedlist = new LinkedList<>();
```

#### Vector
기본적으로 ArrayList와 거의 같고 배열을 사용하며 요소 접근에서 빠른 성능을 보인다.
원래 Vector는 Collection Framwork가 도입되기 전부터 지원하던 클래스이다.
항상 **동기화**(여러 쓰레드가 동시에 데이터를 접근하는 경우 순차적으로 처리)를 지원한다. **멀티 쓰레드에서는 안전**하지만, **단일 쓰레드**에서도 **동기화**를 하기 떄문에 ArrayList에 비해 성능이 약간 느리다.
```
Vector<T> vector = new Vector<>();
```
#### Stack
LIFO(Last in First out) 또는 후입선출로 데이터를 쌓는다.
```
Stack<T> stack = new Stack<>();
```


### Queue 인터페이스
---
**선형 자료구조**로 순서가 있는 데이터를 기반으로 **선입선출(FIFO)** 를 위한 인터페이스이다.
Queue의 가장 앞쪽에 있는 위치를 **head**, 가장 후위에 있는 위치를 **tail**이라고 한다.

Queue를 상속하고 있는 Deque(덱)이라는 인터페이스스가 있는데 **Queue**는 **한쪽 방향**으로만(단방향) **삽입/삭제**가 가능하지만 **Deque**은 Double ended Queue라는 의미로 **양쪽에서 삽입/삭제**가 가능하다.
<img src="https://velog.velcdn.com/images%2Fnnnyeong%2Fpost%2F3244e9fd-82e5-4c52-bef4-dee97640e246%2Fimage.png">
<img src="https://velog.velcdn.com/images%2Fnnnyeong%2Fpost%2Fc412c1f6-9cf2-4fe2-b1c6-b166e2a58c99%2Fimage.png">

<Queue/Deque Interface에 선언된 대표적인 메소드>
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcfpfoQ%2FbtqI66JL8WF%2FYgwfZ2O1HRhm67NK3CovEk%2Fimg.png">

#### LinkedList
List 인터페이스에 있던 클래스와 동일한 클래스이다.
LinkedList는 List를 구현하기도 하지만, Deque도 구현하는데 Deque 인터페이스는 Queue 인터페이스를 상속받기 때때문에 Queue로도 쓰일 수 있다.

Deque 또는 Queue를 LinkedList 처럼 Node 객체로 연결해서 관리하길 원하는 경우 사용한다.
```
Queue<T> queue = new LinkedList<>();
```
#### ArrayDeque
ArrayList 처럼 Object[] **배열**로 구현되어 있는 것은 ArrayDeque이 사용된다.
Deque 인터페이스는 Queue 인터페이스를 상속받기 떄문에 Queue로도 쓰일 수 있다.
```
Deque<T> queue = new LinkedList<>();
```
#### Priority Queue
Queue는 선입선출이지만 priority queue는 **데이터 우선순위를 기반**으로 우선순위가 높은 데이터가 먼저 나온다. 이때 정렬 방식을 지정하지 않았다면 **낮은 숫자**가 **높은 우선 순위**를 가지게 된다.

최대값, 최소값을 꺼내올 때 유용하다. 다만, 사용자가 정의한 객체를 타입으로 쓸 경우 반드시 **Comparator** 또는 **Comparable**을 통해 정렬 방식을 구현해주어야 한다.
* Comparator : 비교 방식을 외부에서 정의할 수 있게 해주는 인터페이스
* Comparable : 객체 자체가 자신의 비교 방법을 정의 할 수 있는 인터페이스

```
ArrayDeque<T> arraydeque = new ArrayDeque<>();
PriorityQueue<T> priorityqueue = new PriorityQueue<>();
 
Deque<T> arraydeque = new ArrayDeque<>();
Deque<T> linkedlistdeque = new LinkedList<>();
 
Queue<T> arraydeque = new ArrayDeque<>();
Queue<T> linkedlistdeque = new LinkedList<>();
Queue<T> priorityqueue = new PriorityQueue<>();
```
### Set 인터페이스
---
**중복을 허용하지 않고, 저장순서가 유지되지 않는** 컬렉션 클래스를 구현하는데 사용된다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkOnus%2Fbtq2feJ4Aio%2FPr86M1nopnP5KOzKN2yMb0%2Fimg.png">

#### HashSet
가장 기본적인 Set 인터페이스의 클래스로 입력 **순서를 보장하지 않으며 중복도 보장되지 않는다**.
이는 **hash**에 의해 **데이터의 위치를 특정**시켜 해당 데이터를 빠르게 **색인(search)** 할 수 있게 만든 것이다. Hash 기능과 Set컬렉션이 합쳐진 것이 HashSet이다.
그렇기 때문에 삽입, 삭제, 색인이 매우 빠른 컬렉션 중 하나다
```
Set<T> strArrSet = new HashSet<>();
```
#### LinkedHashSet
**Link + Hash + Set이 결합된 형태**이다.
LinkedList에서  add() 메서드를 통해 요소들을 넣은 순서대로 연결하여 순서를 보장하는데 Set의 경우 저장 순서를 보장하지 않아 불편함이 있어 **"중복은 허용하지 않으면서 순서를 보장받고 싶은 경우"** 에 사용된다.
```
Set<T> strArrTreeSet = new TreeSet<>();
```
#### TreeSet
Set 인터페이스로 구현되어 **순서를 보장하지 않으며 중복도 보장되지 않으며**
**이진 탐색 트리(Binary Search Tree)** 자료구조의 형태로 데이터를 저장하여 **정렬, 검색, 범위검색**(range search)에 높은 성능을 보인다.
```
Set<T> strArrLinkedSet = new LinkedHashSet<>();
```
### 시간복잡도
---
자바 컬렉션의 주요 클래스들에 대한 시간 복잡도 표이다.
각 컬렉션의 일반적인 연산(추가, 삭제, 검색 등)에 대해 **최선의 경우**, **평균적인 경우**, **최악의 경우**를 기준으로 시간 복잡도를 나타낸다.

**자바 컬렉션 클래스 시간 복잡도 표**

| **컬렉션 클래스**              | **연산**                               | **시간 복잡도 (최선/평균/최악)** | **설명**                                      |
| ------------------------ | ------------------------------------ | --------------------- | ------------------------------------------- |
| **`ArrayList`**          | 추가 (끝에) (`add(E)`)                   | O(1) / O(1) / O(n)    | 배열 끝에 추가. 배열 크기가 넘칠 경우 배열을 복사해야 해서 O(n) 소요. |
|                          | 추가 (중간에) (`add(index, element)`)     | O(n)                  | 삽입할 위치 뒤의 모든 요소를 이동시켜야 함.                   |
|                          | 삭제 (끝에서) (`remove(index)`)           | O(1)                  | 마지막 요소 삭제는 O(1).                            |
|                          | 삭제 (중간에서) (`remove(index)`)          | O(n)                  | 삭제 후 요소들을 한 칸씩 앞으로 이동해야 함.                  |
|                          | 검색 (`get(index)`)                    | O(1)                  | 배열은 인덱스로 직접 접근 가능.                          |
| **`LinkedList`**         | 추가 (끝에) (`add(E)`)                   | O(1)                  | 끝에 추가 시 O(1) 소요.                            |
|                          | 추가 (중간에) (`add(index, element)`)     | O(n)                  | 순차 탐색 후 삽입, 노드 이동 필요.                       |
|                          | 삭제 (끝에서) (`remove()`)                | O(1)                  | 끝에서 삭제 시 O(1).                              |
|                          | 삭제 (중간에서) (`remove(index)`)          | O(n)                  | 삭제 후, 뒤의 노드를 하나씩 이동해야 함.                    |
|                          | 검색 (`get(index)`)                    | O(n)                  | 순차적으로 노드를 탐색해야 함.                           |
| **`HashSet`**            | 추가 (`add(E)`)                        | O(1) / O(1) / O(n)    | 해시 충돌이 발생하면 O(n) 시간이 걸릴 수 있음.               |
|                          | 삭제 (`remove(E)`)                     | O(1)                  | 해시 값을 이용해 빠르게 삭제.                           |
|                          | 검색 (`contains(E)`)                   | O(1)                  | 해시 값을 이용해 빠르게 검색.                           |
| **`TreeSet`**            | 추가 (`add(E)`)                        | O(log n)              | 이진 탐색 트리에서 삽입.                              |
|                          | 삭제 (`remove(E)`)                     | O(log n)              | 트리에서 요소를 삭제해야 하므로 O(log n).                 |
|                          | 검색 (`contains(E)`)                   | O(log n)              | 이진 탐색 트리에서 값을 검색.                           |
| **`HashMap`**            | 추가 (`put(key, value)`)               | O(1) / O(1) / O(n)    | 해시 충돌 시 O(n) 시간이 걸릴 수 있음.                   |
|                          | 삭제 (`remove(key)`)                   | O(1)                  | 해시 값으로 키를 빠르게 찾고 삭제.                        |
|                          | 검색 (`get(key)`)                      | O(1)                  | 해시 값으로 빠르게 값을 검색.                           |
| **`TreeMap`**            | 추가 (`put(key, value)`)               | O(log n)              | 이진 탐색 트리에서 삽입.                              |
|                          | 삭제 (`remove(key)`)                   | O(log n)              | 트리에서 값을 찾아 삭제해야 하므로 O(log n).               |
|                          | 검색 (`get(key)`)                      | O(log n)              | 이진 탐색 트리에서 값을 찾는 데 O(log n) 소요.             |
| **`LinkedHashMap`**      | 추가 (`put(key, value)`)               | O(1)                  | 해시 값으로 빠르게 삽입.                              |
|                          | 삭제 (`remove(key)`)                   | O(1)                  | 해시 값으로 키를 빠르게 삭제.                           |
|                          | 검색 (`get(key)`)                      | O(1)                  | 해시 값을 이용한 빠른 검색.                            |
| **`PriorityQueue`**      | 추가 (`offer(E)`)                      | O(log n)              | 힙에 값을 추가할 때 O(log n) 시간이 걸림.                |
|                          | 삭제 (`poll()`)                        | O(log n)              | 힙에서 우선순위가 높은 값을 삭제할 때 O(log n) 소요.          |
|                          | 검색 (`peek()`)                        | O(1)                  | 우선순위 큐에서 가장 큰(작은) 값에 접근할 때 O(1) 소요.         |
| **`Stack`**              | 추가 (`push(E)`)                       | O(1)                  | 스택의 top에 데이터를 추가하는 연산은 O(1).                |
|                          | 삭제 (`pop()`)                         | O(1)                  | 스택의 top에서 데이터를 삭제하는 연산은 O(1).               |
|                          | 검색 (`peek()`)                        | O(1)                  | 스택의 top에 있는 값을 확인하는 연산은 O(1).               |
| **`Deque` (LinkedList)** | 추가 (`addFirst(E)`, `addLast(E)`)     | O(1)                  | 양쪽 끝에서 빠르게 추가 가능.                           |
|                          | 삭제 (`removeFirst()`, `removeLast()`) | O(1)                  | 양쪽 끝에서 빠르게 삭제 가능.                           |
|                          | 검색 (`getFirst()`, `getLast()`)       | O(1)                  | 양쪽 끝에서 빠르게 값을 가져올 수 있음.                     |

## 참조
---
[자바 [JAVA] - 자바 컬렉션 프레임워크](https://st-lab.tistory.com/142)
[Set 인터페이스](https://ssdragon.tistory.com/69)
[[Java] Collection Framework(List, Map, Set)의 인터페이스와 구현체 이해하기 - 1 : 정의 및 예시](https://adjh54.tistory.com/138)