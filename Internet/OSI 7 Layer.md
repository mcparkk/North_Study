## 네트워크
---
: 컴퓨터나 기타 기기들이 리소스를 공유하거나 데이터를 주고 받기 위해 유선 혹은 무선으로 연결된 통신 체계

기능
- 애플리케이션 사이에서 목적에 맞는 통신 방법을 제공
- 애플리케이션 사이에서 안전하게 데이터를 전송하는 방법
- 네트워크 간의 최적의 통신 경로 결정
- 애플리케이션이 동작하고 있는 호스트 사이에서 목적지까지 데이터를 전송
- 목적지로 데이터를 전송하기 위해서는 여러 노드를 거치는데, 이때 노드 사이의 데이터 전송 수행

위와 같은 통신 기능이 제대로 동작하기 위해서는 참여자들 사이에서 약속된 통신 방법이 있어야 한다.

네트워크 프로토콜
: 네트워크 통신을 하기 위해서 통신에 참여하는 주체들이 따라야하는 형식, 절차, 규약

위 네트워크 기능들이 단 하나의 프로토콜로 구현될 수 없어 기능별로 모듈화를 하여 OSI 7 layer 탄생


## OSI 7 Layer
---
: 범용적인 네트워크 구조

<img src="https://blog.lael.be/wp-content/uploads/2014/10/j8.gif">
#### application layer (응용 계층)
유저가 이용하는 응용 프로그램과 직접 관련되어 서비스를 제공한다.
최상위 계층으로 사용자에게 직접적으로 보여지는 부분이며, 웹서버나 웹브라우저에게 직접적으로 데이터를 전송/수신할 때 이용되는 계층이다.

애플리케이션 목적에 맞는 프로토콜을 사용한 통신 방법 제공한다.
- HTTP : 한 애플리케이션이 다른 애플리키이션과 통신을 통해 사용자에게 웹 페이지를 노출 시키고 싶은 경우
- FTP : 파일을 서버에 업로드, 다운로드하는 어플리케이션을 만들고 싶은 경우
- DNS :  youtube.com 과 같은 도메인을 ip주소로 바꾸고 싶은 경우
- SMTP : 이메일을 주고 받는 기능을 구현하고 싶은 경우

#### presentation layer(표현 계층)
데이터 표현과 변환을 담당하여 데이터를 응용 계층으로 전달하거나, 그 반대의 과정을 수행한다.
이때 데이터를 안전하게 사용하기 위해 암호화/복호화도 진행한다.

#### session layer(세션 계층)
애플리케이션 간의 통신을 하기 위한 세션을 운영체제를 통해 확립, 유지, 중단하는 작업을 수행한다.
즉, 애플리케이션 간의 접속을 설정, 유지하고 끊어질 경우 데이터를 재전송하거나 연결을 복구한다.
_세션(Session)이란?
- _네트워크 환경에서 사용자 간 또는 컴퓨터 간의 대화를 위한 논리적 연결.
- _프로세스들 사이에 통신을 수행하기 위해서 메시지 교환을 통해 서로를 인식 한 이후부터 통신을 마칠 때까지의 기간.

#### transport layer(전송 계층)
양 종단간 신뢰성 있는 연결을 담당하는 계층이다.
송신자와 수신자가 정확하고 신뢰성있는 통신을 하기 위해 오류 검출/복구, 흐름제어, 중복 검사 등의 기능을 수행한다.
Prot 번호를 식별자로 어떤 프로토콜을 사용하여 데이터를 목적지 애플리케이션으로 전송될지 판독한다.

대표적인 전송 계층 프로토콜로는 TCP(안정적이고 신뢰할 수 있는 데이터 전송 보장) / UDP(필수 기능만 제공) 가 있다.

> 장비 - 게이트웨이, 로드밸런서
> 데이터 단위 - 세그먼트
#### network layer(네트워크 계층)
호스트(인터넷에 연결된 컴퓨터) 간의 통신 담당하며 네트워크 간 최적의 경로를 바탕으로 데이터를 전송하기 위한 계층이다. 이러한 탐색 과정은 라우팅(Routing)이라고 한다.

IP 주소를 사용하여 목적지에 도달하기 위한 경로를 선택하고, 경로에 따라 패킷을 전달한다.

> 장비 - 라우터, 공유기, 스위치(L3 스위치)
> 데이터 단위 - 패킷

#### data link layer(데이터 링크 계층)
인접한 두 장치간에 데이터를 주고 받을 수 있도록하는 계층이다.
MAC 주소를 기반으로 직접 연결된 노드간의 통신 담당하며 데이터의 오류와 흐름을 관리하는 기능이 있다.
( ARP : IP를 MAC으로 변환헤주는 프로토콜 )

> 장비 - 브릿지, 스위치
> 데이터 단위 - 프레임

#### physical layer(물리 계층)
네트워크 전송 매체를 통해 데이터를 전송하기 위한 기초적인 기능을 수행한다. 전기적, 물리적 기계적인 특성을 결정하고 데이터를 전기 신호, 광 신호 전파 등으로 변환한다.

컴퓨터는 전기가 흐른다(1), 흐르지 않는다(0) 신호로 데이터를 정의한다.
전자기파는 0~무한대의 주파수 범위를 갖기 때문에 0과 1로 이루어진 전기적 신호를 통과 시킬 수 있는 전선이 없다. 따라서 이러한 전기적인 신호(0,1)를 곡선 형태의 아날로그 신호로 변경하는 인코딩, 디코딩 과정이 필요하다.

> 장비 - 허브 , 리피터
> 데이터 단위 - bit

<img src="https://images.velog.io/images/jeongs/post/814a73d3-02ad-47aa-ad46-d161b20f4e73/1%EA%B3%84%EC%B8%B5(2).png">


## encapsulation & decapsulation
---
데이터를 전송하는 경우 7계층에서 1계층으로 가게된다. 이 과정에서 캡슐화를 하게 되는데 각 계층의 정보를 해더에 담아서 최종 전송되게 된다.

ex. Message를 전송하려는 경우
application layer                       <u>| H | M |</u>
presentation layer                     <u>| H |</u> H | M |
session layer                              <u>| H |</u> H | H | M |
transport layer                           <u>| H |</u> H | H | H | M |
network layer                             <u>| H |</u> H | H | H | H | M |
data link layer                             <u>| H |</u> H | H | H | H | M <u>| T |</u>   *T : 트레일러 - 전송 후에 에러 여부 확인*
physical layer                              위 정보들을 가지고 bit 단위로 전송

![[osi7_capsulation.png]]


## TCP / IP 모델
---
현대의 인터넷은 OSI 모델이 아니라 TCP/IP 모델을 따르고 있다.
-> 시장 점유 싸움에서 이김

<img src="https://www.rtautomation.com/wp-content/uploads/2023/01/osi-tcpip-diagram.jpg">
#### 참고사항
---

> [!note] 참고사항
> > OSI 7 계층은 네트워크 구성을 설명하기 위해 개념적으로 남아있는  개념이고, 실제로는 TCP/IP 4계층이 사용된다.
> > TCP/IP 4계층에서는 세션 계층, 표현 계층을 모두 응용 계층에 포함하여 생각한다.




## 참조
---

[OSI 7 계층 파해치기 - 티스토리](https://mundol-colynn.tistory.com/167)
[네트워크-OSI-7-계층-그림과-함께-이해하기 - 티스토리](https://velog.io/@jeongs/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-OSI-7-%EA%B3%84%EC%B8%B5-%EA%B7%B8%EB%A6%BC%EA%B3%BC-%ED%95%A8%EA%BB%98-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0)
[MAC주소, IP주소, Port번호가 식별하는 것 - youtube](https://www.youtube.com/watch?v=JDh_lzHO_CA)
[프로토콜과 OSI 7 layer 설명 - youtube](https://www.youtube.com/watch?v=6l7xP7AnB64)
[OSI 7 Layer - youtube](https://www.youtube.com/watch?v=1pfTxp25MA8)