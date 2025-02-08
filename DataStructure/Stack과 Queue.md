
## 스택 (Stack)
---
<img src="https://blog.kakaocdn.net/dn/by1qnT/btqBE1v1UlX/zbnXdYnGAXhMYbcDCca6WK/img.png" height=250 width=250>
스택은 데이터를 쌓아 올리는 형태의 **후입선출**(LIFO, Last-In-First-Out)  구조이다. 
같은 구조와 크기의 자료를 정해진 방향으로만 쌓을 수 있으며, top으로 정한 곳을 통해서만 접근할 수 있다. 
시간 순서에 따라 데이터가 쌓이는 스택의 특징으로 가장 마지막에 삽입된 데이터가 가장 먼저 삭제된다. 
- push : top을 통해 데이터 삽입하는 연산
	- 오버플로우 상태(Overflow condition) : 스택이 찬 상태에서 데이터를 넣는 경우
- pop : top을 통해 데이터 삭제하는 연산
	- 언더플로우 상태(Underflow condition) : 비어있는 스택에서 데이터를 꺼내려고 하는 경우

**스택의 활용 예시**
- 웹 브라우저 방문기록(뒤로가기)
- 실행 취소(undo)
- 역순 문자열 만들기
- 후위 표기법 계산

스택 오버플로우
스택 자료구조에서 **스택 오버플로우**는 **정해진 크기의 스택에 데이터를 삽입하려고 할 때, 스택의 용량을 초과**할 경우 발생하는 상황이다.
예를 들어, 스택이 고정 크기로 구현되어 있을 때, 더 이상 데이터를 넣을 공간이 없으면 오버플로우가 발생한다.
##### 스택 자료구조에서의 스택 오버플로우
자바의 Stack 클래스나 ArrayList 기반의 스택 구현에서는 크기가 동적으로 확장되기 때문에 실제 실행 환경에서는 크기 초과 문제를 자동으로 처리하기 때문에 **스택오버플로우가 발생하지 않는다.**

자바의 Stack 클래스는 **Vecto를 상속**하고 있기 때문에 내부적으로 **배열 기반의 동적 크기 조정**을 지원하는 Vector를 사용하여 데이터를 저장한다.
+ArrayList 클래스도 같은 구조로 스택 동작을 구현할 수 있다.
- Stack 클래스, ArrayList 클래스 모두 동적 크기 조장이 가능한 배열 기반 자료구조이다.

Stack 클래스
- 스택 구조가 명확히 필요한 경우, 후입선출(LIFO) 원칙을 따라야 할 때 사용.
- 멀티스레드 환경에서 동기화가 필요한 경우.
ArrayList 클래스
- LIFO 동작이 필요한 경우 스택을 구현하기 위해서 사용 가능.
- 성능을 중시하거나, 멀티스레드 환경에서 동기화를 직접 처리할 수 있는 경우.
*ArrayList로 스택을 구현하는 경우  push(), pop(), peek() 등의 메서드 직접 구현 필요*

##### 재귀 호출에서의 스택 오버플로우
자바에서 **스택 오버플로우**는 주로 **재귀 호출**로 인한 문제이다.
재귀 함수가 너무 깊게 호출되면, 자바의 **호출 스택(Call Stack)이 가득 차서** 더 이상 함수를 호출할 수 없게 된다. 이때 발생하는 오류가 "StackOverflowError"이다.



## 큐 (Queue)
---
<img src="https://velog.velcdn.com/images/mjieun/post/4a21cf90-6c3e-4a78-9637-acec7e5f60ed/image.png" height=250 width=250>
데이터가 입력된 순서대로 처리하는 형태의 **선입선출**(FIFO, First In First Out) 구조이다.
데이터의 입구와 출구가 나뉘어져 있어, **리어(Rear)** 에서 데이터 삽입이, **프론트(Front)** 에서 데이터 삭제가 이루어 진다. 
- 인큐(Enqueue) : 데이터 삽입
- 디큐(Dequeue) : 데이터 삭제

**큐의 활용 예시**
- 인쇄 대기열
- 은행 업무
- 프로세스 관리
- 너비 우선 탐색(BFS, Breadth-First Search) 구현


## 참조
---
gpt 질의
- 스택 클래스를 사용하는 경우 스택오버플로우가 발생할 수 있는건지 알려줘
  [자료구조 스택과 큐 - 티스토리](https://dev-records.tistory.com/entry/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EC%8A%A4%ED%83%9DStack%EA%B3%BC-%ED%81%90Queue)
  [Stack & Queue (스택과 큐) - 티스토리](https://jhbljs92.tistory.com/entry/1-Stack-Queue-%EC%8A%A4%ED%83%9D%EA%B3%BC-%ED%81%90)