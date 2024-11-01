## HTTP란?

**HTTP (HyperText Transfer Protocol)** 은 웹 브라우저와 웹 서버 간에 데이터를 주고받기 위한 **통신 프로토콜**로 1990년대에 처음 도입된 HTTP는 주로 **하이퍼텍스트(HyperText)**, 즉 웹 페이지(HTML)를 주고받는 데 사용되었다. 클라이언트(브라우저)가 서버에 요청을 보내면 서버는 이에 대한 응답으로 요청된 리소스를 전송하는 방식이다.

- **클라이언트-서버 모델**: HTTP는 클라이언트(예: 웹 브라우저)가 서버에 요청을 보내면, 서버가 이에 응답하는 구조로 작동한다.
- **무상태 프로토콜**: HTTP는 **Stateless**(무상태) 프로토콜로, 각 요청이 독립적이며 이전 요청과 연결되지 않는다. 서버는 클라이언트의 상태를 저장하지 않는다.

### Q. 해당 원칙의 설계 배경은?

**HTTP는 World-Wide-Web의 최초 목적인 과학자들 간의 정보 공유를 위해 설계** 되었고, 당시 컴퓨터 자원의 한계 때문에 최대한 단순하게 설계 되어야 했다. 서버, 클라이언트 모두 성능이 제한적이었기 때문에 복잡한 프로토콜의 구성이 어려웠으므로 지속적인 연결을 관리하거나, 복잡한 상태를 유지하는 것이 비용상 제한적이었기 때문에 가장 단순한 **요청-응답**(클라이언트-서버 모델) 형태를 가지게 하고, **무상태**(Stateless)를 가지도록 설계되었다.

### Q. 웹소켓과 같은 실시간 프로토콜은 HTTP 위에서 동작하는가?

HTTP는 **단순한 요청-응답 모델**로 실시간 데이터를 처리하는데는 제한이 있다. 이를 통해 웹소켓(WebSocket) 프로토콜이 등장하게 되었고 **HTTP를 기반으로 연결을 시작**하지만 HTTP와 다른 방식으로 **지속적인 데이터 스트림을 유지**한다.

```http
GET /chat HTTP/1.1
Host: example.com
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
```

위와 같은 요청을 통해 **웹소켓 프로토콜로의 전환**이 승인되면 웹소켓 연결로 업그레이드 되며 **기존 HTTP 연결을 지속적이고 양방향 통신이 가능한 상태로 전환**한다.

### Q. 그런데 지금은 HTTP 프로토콜에서도 상태 유지 되잖아요? (로그인 등)

**HTTP 프로토콜 자체**는 클라이언트와 서버 간의 요청을 **독립적으로** 처리하며, **이전 요청의 상태를 기억하지 않는다**. 서버는 **각 요청을 처음 온 요청인 것처럼 처리**한다.

그러나 로그인과 같은 기능에서 **서버가 세션을 통해 상태를 기억하는 것**은 **HTTP 프로토콜의 무상태성**과는 직접적인 관련이 없다. **HTTP 프로토콜**은 여전히 **무상태(Stateless)**로 설계되어 있지만, **애플리케이션 레벨**에서는 **세션, 쿠키, JWT**와 같은 상태 유지 메커니즘을 사용하여 **상태 관리를 구현**할 수 있다.

즉, 이는 **HTTP의 무상태성 위에 추가적으로 구현된 상태 관리 기법**으로, 클라이언트의 요청에 상태 정보를 포함시키는 방식으로 동작한다.


## 버전 별 HTTP의 특징

### HTTP/0.9 - 1991년

```http
GET /mypage.html

<html>
	A very simple HTML page!
</html>
```

가장 처음 개발된 매우 간단한 프로토콜로 **단순하게 클라이언트가 요청을 보내면 서버가 HTML 문서를 응답**하는 구조다.

- 텍스트 기반 요청
	- `GET /index.html`과 같은 텍스트 기반 요청을 사용했고, 최초에는 단일 명령인 `GET`만 지원했다.
- HTML 문서만 응답
	- 서버는 클라이언트의 요청에 따라 **단일 HTML 문서**만 응답했다. 이미지, 스크립트, CSS와 같은 다른 리소스를 전송할 방법이 없었고, MIME 타입과 같은 데이터 형식 정의도 없었다.
- Header 없음
	- HTTP/0.9에는 **요청과 응답에 헤더가 존재하지 않음**. 요청은 단순히 URL을 지정하고, 서버는 해당 HTML 파일을 클라이언트에 전달하는 방식이었다.

이로 인해 HTML 외 데이터는 전송하지 못하고, 확장성이 매우 제한적이었다. 또한 독립적인 각 요청들로 인해 연결을 재활용할 수 없고 서버-클라이언트 간의 지속적인 연결 유지가 불가능했다.

### HTTP/1.0 - 1996년

```http
GET /mypage.html HTTP/1.0
User-Agent: NCSA_Mosaic/2.0 (Windows 3.1)

200 OK
Date: Tue, 15 Nov 1994 08:12:31 GMT
Server: CERN/3.0 libwww/2.17
Content-Type: text/html

<html>
	Text
	<IMG SRC="/myimage.gif">
</html>
```

```http
GET /myimage.gif HTTP/1.0
User-Agent: NCSA_Mosaic/2.0 (Windows 3.1)

200 OK
Date: Tue, 15 Nov 1994 08:12:32 GMT
Server: CERN/3.0 libwww/2.17
Content-Type: text/gif
(image content)
```

이후 웹이 급격하게 성장하면서 등장한 HTTP의 **첫 번째 정식 버전**으로 1996년에 표준화 되었다.

- 헤더 도입
	- 클라이언트와 서버가 데이터를 자세히 설명하고 제어 가능하게 되었다. 서버는 `Content-Type`과 같은 헤더를 사용해 데이터 형식을 명시할 수 있게 되었고, 각종 멀티미디어 데이터나 JSON 등 다양한 형식을 지원하 되었다.
- 다양한 요청 메서드 추가
	- 기존 `GET`만 지원하던 초기 버전에 비해 `POST`, `HEAD`, `PUT`, `DELETE`와 같은 다양한 메서드를 추가하여 클라이언트가 서버의 리소스를 조작하는 등 다양한 작업을 할 수 있게 되었다.
- 상태 코드
	- 서버가 클라이언트의 요청에 응답할 때 요청 성공 여나 오류 상태를 전달할 수 있도록 상태 코드가 도입되었다.
- 버전 정보
	- 각 요청들은 버전 정보를 포함되어 전송된다.

HTTP 헤더 개념은 요청과 응답 모두 도입되어 [[용어 정리#메타 데이터|메타 데이터]] 전송이 가능해졌고, 이를 통해 프로토콜이 극도로 유연해지고 확장성이 높아졌다. 그러나 HTTP/1.0은 여전히 **요청-응답마다 새로운 연결을 열고 닫는 방식**이었기 때문에 한 페이지에 여러 리소스가 필요한 경우(여러개의 이미지, CSS 등) 각 리소스마다 새로운 연결을 열어야 했고, 이는 네트워크 자원을 비효율적으로 사용하게 했다.

### HTTP/1.1 - 1997년

**현재 가장 널리 사용되는 HTTP 버전**으로 이전 버전의 한계를 해결하고 성능 개선 및 다양한 기능이 추가되었다.

- 지속적인 연결
	- 기본적으로 **지속적인 연결**(Persistent Connection)을 지원하여 하나의 연결로 여러 요청과 응답을 주고 받을 수 있게 되었다.
- 파이프라이닝
	- 클라이언트가 연속적인 요청을 한번에 보낼 수 있는 파이프라이닝(Pipelining)이 도입되었으나 이는 브라저나 서버에서 제대로 지원되지 않아 자주 사용되지는 않았다.
- 캐시 제어
	- 캐시를 더 효과적으로 관리할 수 있도록 `Cache-Control`, `ETag` 등의 헤더가 도입되었다.
- 가상 호스팅
	- `Host` 헤더를 통해 여러 도메인이 같은 IP 주소를 공유할 수 있는 가상 호스팅을 지원한다.

HTTP/1.1은 여전히 **평문 통신**을 사용했기 때문에 **스니핑이나 중간자 공격에 취약**했다. 또한 성능은 개선되었지만 여전히 **한 연결당 하나의 리소스를 요청하는 구조로 인해 네트워크 지연** 문제가 있었다.

### HTTP/2 - 2015년

HTTP/1.1의 성능 문제를 해결하고자 **SPDY** 프로토콜을 기반으로 2015년에 표준화된 HTTP 버전이다. HTTP/1.1과의 하위 호환성을 유지하는 동시에 성능과 효율성이 개선되었다.

- 멀티플렉싱
	- 하나의 연결에서 여러 요청과 응답을 **동시에 처리**할 수 있게 되었다. = 병렬 처리 가능.
- 헤더 압축
	- **HPACK** 알고리즘을 사용해 요청 및 응답에 포함된 헤더를 압축하고, 이전 버전의 반복적으로 전송되던 헤더를 효율적으로 압축하여 전송 속도를 높였다.
- 서버 푸시
	- 클라이언트가 요청하지 않은 리소스를 서버가 **미리 전송**할 수 있다. 클라이언트가 HTML 파일을 요청할 때 서버가 자동으로 문서 내에 포함된 CSS 및 Javascript 파일을 푸시하여 페이지 로딩 시간을 줄일 수 있다.
- 바이너리 프로토콜
	- HTTP/2는 텍스트 기반이 아닌 **바이너리 프레이밍** 방식을 채택하여 데이터 전송 효율을 높였다. 이로 프로콜 해석이 간소화되고 데이터 전송 속도가 개선되었다.

**연결 재활용**으로 네트워크 자원을 효율적으로 사용하고, 페이지 로딩속도를 크게 단축시키고 멀티플렉싱과 헤더 압축을 통해 데이터 전송시의 병목을 줄였다. 그러나 여전히 **TCP**를 기반으로 하기 때문에 TCP에서 패킷 손실이 발생하면 해당 패킷을 복구 할때까지 모든 요청이 대기(Head-ofLine Blocking)하는 문제가 있다.

### HTTP/3 - 2020년 (초안 표준)

**HTTP/2의 TCP 한계를 극복**하기 위해 **UDP 기반의 QUIC(Quick UDP Internet Connection)** 프로토콜을 사용한 최신 버전으로 2020년에 초안으로 표준화 되었다.

- QUIC 프로토콜 기반
	- TCP가 아닌 UDP를 기반으로 동작하여 **빠른 연결 설정**과 **데이터 전송속도**를 지원한다. TLS 암호화와 TCP의 기능을 통합하여 UDP 위에서 동작하도록 설계되었다.
- 0-RTT 연결 설정
	- QUIC은 0-RTT 연결 설정을 통해 클라이언트가 기존 연결 경험이 있을 때 처음 요청 시점부터 데이터를 전송해 연결 설정 시간을 최소화하고 빠른 초기 연결을 제공한다.
- 패킷 기반 데이터 전송
	- QUIC은 각 패킷이 독립적으로 처리되어, 패킷 손실 시에도 다른 패킷이 정상적으로 전송 및 처리하는 방식을 통해 이전 버전의 Head-of-Line Blocking 문제가 해결하였다.
- 내장된 암호화 (TLS 1.3)
	- HTTP/3는 **기본적으로 TLS 1.3**을 사용하여 모든 통신이 암호화된다. 암호화와 연결 설정이 QUIC 프로토콜에 통합되어 있어 보안과 성능 모두 개선되었다.

연결 설정 속도와 데이터 전송 효율이 HTTP/2보다 뛰어나며, 패킷 손실이 발생해도 성능에 영향을 미치지 않는다. 또한 TCP 대신 UDP를 사용함으로써 이전의 Head-of-Line Blocking 문제를 해결하였다.

### Q. HTTP/1.1의 Persistent Connection과 HTTP/2의 Multiplexing은 무슨 차이?

| 기능          | HTTP/1.1 (Persistent Connection) | HTTP/2 (Multiplexing)          |
| ----------- | -------------------------------- | ------------------------------ |
| 연결 수        | 하나의 연결로 여러 요청/응답 가능              | 하나의 연결로 여러 요청/응답 가능            |
| 요청/응답 처리 방식 | **순차 처리**: 한 번에 하나의 요청/응답        | **병렬 처리**: 여러 요청/응답을 동시에 처리    |
| 데이터 전송 방식   | 텍스트 기반의 요청/응답                    | **바이너리 프레임**으로 요청/응답을 전송       |
| 파이프라이닝      | 일부 지원하지만, 브라우저와 서버의 제한으로 제한적     | 필요 없음, 멀티플렉싱으로 병목 현상 해결        |
| 성능과 효율성     | 요청/응답 지연으로 성능 저하 가능성 있음          | 멀티플렉싱으로 네트워크 자원 효율적 사용 및 성능 개선 |

### Q. 스프링 기반의 Web Application에 HTTP/2, HTTP/3를 적용할 경우

HTTP 프로토콜은 백엔드 프레임워크와는 별개로 WAS나 리버스 프록시의 설정에 종속되는 개념이므로 **내장 Tomcat**을 사용하는 스프링 부트와 같은 경우 추가로 설정할 수 있다.

#### HTTP/2를 적용하는 경우

HTTP/2는 대부분의 **주요 서버**(예: Tomcat, Jetty, Undertow)에서 지원하며, 이를 적용하기 위해 SSL/TLS 설정이 필요하다. HTTP/2는 기본적으로 **TLS 기반(HTTPS)** 에서만 동작하기 때문에, HTTPS 설정을 먼저 구성한 후 HTTP/2를 활성화해야 한다.

- 프로퍼티 설정

```yml
server:
  http2:
    enabled: true
  ssl:
    enabled: true
    key-store: classpath:keystore.p12
    key-store-password: your_password
    key-store-type: PKCS12
```

- SSL 인증서 준비

HTTP/2는 HTTPS에서만 지원되므로, **SSL 인증서**를 요구한다. 개발 환경에서는 **self-signed certificate**를 사용할 수 있지만, 운영 환경에서는 **공인된 인증서(CA)** 를 사용해야 한다.

스프링 부트에서 Tomcat을 사용하는 경우 위와 같이 설정하여 사용할 수 있다. 인증서를 설정할 때는 **JKS** 또는 **PKCS12** 형식의 키스토어 파일을 사용해야 하며, 이를 프로퍼티에서 참조한다.

#### HTTP/3를 적용하는 경우

HTTP/3는 UDP 기반의QUIC 프로토콜을 사용하기 때문에 스프링 부트의 내장 WAS에서는 직접 지원하지 않는다. HTTP/3를 스프링 부트 어플리케이션에서 사용할 경우 **리버스 프록시 서버**를 통해 설정해야 한다.

## HTTP 연결 과정

네트워크 전반에 대한 이해를 요구하며 우리가 흔히 웹에 접속하는 순서를 요약하면 다음과 같다.

- **DNS 조회**로 서버 IP 주소를 확인.
- **TCP 3-Way Handshake**로 연결 설정.
- (HTTPS의 경우) **SSL/TLS Handshake**로 암호화된 통신 설정.
- **HTTP/HTTPS 요청**을 통해 클라이언트가 리소스를 요청.
- **서버의 응답**으로 클라이언트가 리소스를 수신.
- **브라우저가 리소스 로딩 및 렌더링**.
- **TCP 4-Way Handshake**로 연결 종료.

### 3-Way Handshake

![](https://i.imgur.com/RLhQDzA.png)

TCP 연결을 설정할 때 클라이언트-서버 간에 세 번의 패킷을 교환하는 과정으로 신뢰할 수 있는 연결을 설정하기 위해 필요하다.

1. SYN (Synchronize)
	- 클라이언트가 서버에 연결을 요청하여 **SYN 패킷**을 보며 여기에는 초기 **시퀀스 번호**를 포함한다.
	- 클라이언트의 상태는 `SYN_SENT`.
2. SYN-ACK (Synchronize-Acknowledge)
	- 서버는 클라이언트의 요청을 받은 후 응답으로 **SYN_ACK 패킷**을 보낸다. 서버의 패킷에는 자신의 시퀀스 번호와 클라이언트의 시퀀스 번호에 대한 **ACK 번호**를 포함한다.
	- 서버의 상태는 `SYN_RECEIVED`.
3. ACK (Acknowledge)
	- 클라이언트는 서버의 응답을 받고 최종적으로 **ACK 패킷**을 전송한다. 
	- 서버와 클라이언트의 상태가 `ESTABLISHED`.

이를 통해 클라이언트와 서버는 서로의 시퀀스 번호와 ACK을 확인하고, 연결이 설정된다.

### 4-Way Handshake

![](https://i.imgur.com/sLrldB0.png)

4-Way Handshake는 TCP 연결을 해제할 때 클라이언트와 서버 간에 네 번의 패킷을 교환하는 과정으로 연결을 안전하게 종료하고, 사용하지 않는 리소스를 해제한다.

1. FIN (Finish) - Client Side
	- 클라이언트가 연결을 종료하기 위해 **FIN 패킷**을 서버에 전송한다. 
2. ACK (Acknowledge)
	- 서버는 FIN 패킷을 받고, 클라이언트에 **ACK 패킷**을 보낸다. 이 때 서버는 아직 데이터를 전송할 수 있고, 연결은 부분적으로 종료된다.
3. FIN - Server Side
	- 서버는 전송할 데이터가 모두 끝났다면 **FIN 패킷**을 클라이언트에게 보낸다.
4. ACK
	- 클라이언트는 FIN 패킷을 받고, 다시 서버에 **ACK 패킷**을 보낸다. 이로써 연결이 완전히 종료된다.

만약 서버 쪽에서 전송한 패킷 중 패킷 유실이나 재전송으로 인해 서버의 FIN 패킷보다 늦게 도착하는 경우를 대비해 클라이언트는 서버로부터 FIN 패킷을 수신하더라도 일정 시간동안 세션을 남겨놓고 잉여 패킷을 대기하는데, 이를 `TIME_WAIT`이라고 한다.

## HTTP에서 HTTPS로 발전한 과정

**SSL (Secure Sockets Layer)** 는 1990년대 중반 전자상거래와 같은 보안이 필요한 서비스가 급증하게 되면서 각 종 보안이 필요한 서비스를 위해 개발되었고, 이후 여러 문제점을 개선하면서 **TLS (Transport Layer Security)** 로 발전하게 되었다.

**HTTPS (HyperText Transfer Protocol Secure)** 는 **HTTP**에 **SSL/TLS(Transport Layer Security)** 를 추가하여 통신을 암호화한 버전이다. **HTTP**는 데이터를 **암호화하지 않고 평문(Plain Text)으로 전송**하기 때문에 보안에 취약하며, 이를 통해 발생할 수 있는 주요 문제점은 아래와 같다.

1. **[[용어 정리#스니핑|도청(스니핑, Sniffing)]]**: HTTP는 평문으로 데이터를 전송하므로 네트워크 중간에서 데이터를 가로챌 수 있다. 이를 통해 사용자 이름, 비밀번호, 민감한 데이터가 노출될 위험이 있다.
    
2. **[[용어 정리#중간자 공격|중간자 공격(Man-in-the-Middle Attack, MITM)]]**: 공격자가 네트워크 중간에서 통신을 가로채고 조작하여 악성 데이터를 주입할 수 있다.
    
3. **데이터 무결성 문제**: HTTP는 데이터의 변경 여부를 확인하지 않기 때문에, 중간에서 데이터가 변경되어도 이를 확인할 방법이 없다.
    

**HTTPS**는 이러한 문제를 해결하기 위해 **암호화를 통해 데이터 기밀성을 보장**하고, **데이터 무결성**과 **서버 인증**을 제공한다.

### SSL/TLS 버전 요약

- **SSL 2.0**: 최초의 상용 버전이지만 보안 문제로 금방 대체됨.
- **SSL 3.0**: 널리 채택되었지만 여전히 보안상 취약점이 있었음.
- **TLS 1.0**: SSL 3.0을 표준화하고 보안을 강화하여 새로운 표준으로 자리 잡음.
- **TLS 1.1 및 TLS 1.2**: 보안성을 추가적으로 강화하고, 확장성을 고려한 개선이 이루어짐. (가장 많이 사용되는 버전)
- **TLS 1.3**: 최신 보안 기술과 최적화된 구조를 적용하여 현대의 보안 요구사항을 충족시키는 프로토콜로 발전.

> [!info] SSL은 더 이상 사용되지 않는다
>
> 최초의 TLS 1.0 버전은 SSL 3.0을 기반으로 보안성을 강화하 표준화한 버전으로, 이후 더 이상 SSL은 유지되지 않고 TLS가 새로운 표준이 되었다.
> 
> 그럼에도 SSL/TLS라고 혼용하는 것은 SSL이라는 용어가 이 보안 프로토콜의 대명사격으로 인식되었기 때문이며 이를 포괄적으로 표현하기 위해 SSL/TLS와 같은식으로 표기된다.

## HTTPS 연결 과정

**HTTP**와 **HTTPS**는 단순히  **SSL/TLS** 암호화 프로토콜을 하는가의 여부만 차이가 있다. HTTPS 통신 과정에서의 주요 단계는 **SSL/TLS Handshake**로 이 과정을 통해 클라이언트와 서버는 **암호화된 통신을 위한 키를 교환**하고, 안전한 연결을 설정한다.

### SSL/TLS Handshake

비대칭키 <- 공개키, 비밀키

공개키 - 암호화만 할 수 있음
비밀키 - 복호화를 할 수 있음

1. 클라이언트 -> 서버 - 내가 쓸수있는 암호화 방식, TLS 버전 리스트 제안
	1. 암호화 방식, TLS 버전 리스트
2. 서버 -> 클라이언트 - 리스트에서 하나를 채택 후 인증서와 함께 클라이언트로 전송
	1. 인증서 - 루트 인증서 서명, 해당 서버의 공개키, 도메인, 인증서 체인
	2. 인증서랑 서버의 공개키
	3. 확인되지 않은 인증서 <- 이거 신뢰할거임? - 응 신뢰할게
3. 클라이언트 -> 서버 - 클라이언트는 자신의 세션 키를 무작위로 만들어서 서버의 공개키로 암호화 후 서버에 전송
	1. 암호화된 세션키
		1. **중간자가 복호화 할 수 가 없음**
4. 서버 - 세션 키를 복호화함
5. 이후 모든 요청 응답을 암호화하고 서로가 가지고 있는 세션키로 복호화해서 요청을 주고 받는다

![](https://i.imgur.com/SGtEbXU.png)

만약 접속하는 웹사이트가 HTTPS를 사용하는 경우, TCP 연결이 설정된 후 SSL/TLS 핸드셰이크가 이루어진다(위 그림의 노란색 부분).  이 과정에서 클라이언트와 서버는 암화된 통신을 설정한다.

1. 클라이언트 헬로(Client Hello)
	- 클라이언트는 서버에 **지원 가능한 암호화 방식과 TLS 버전을 제안하는 패킷**을 보낸다.
2. 서버 헬로(Server Hello)
	- 서버는 클라이언트가 제안한 암호화 방식 중 하나를 선택하고, **SSL/TLS 인증서**를 클라이언트에 전송한다. 이 인증서는 서버의 공개키를 포함하고 있다.
3. 키 교환
	- 클라이언트는 서버의 공개 키를 사용해 **세션 키**를 암호화하여 서버에 전송한다. 서버는 이 세션 키를 복호화하여 이후 통신에 **대칭키**로 사용된다.
4. 완료
	- 클라이언트와 서버는 세션 키로 암호화된 통신을 시작한다.

만약 서버 간의 공통 암호화 방식이 없거나 호환 가능한 TLS 버전이 없으면 핸드셰이크는 실패한다.

### Q. 브라우저에서 특정 프로토콜의 포트를 명시하지 않아도 자동으로 전환되는 이유

HTTP는 **기본적으로 80포트**, HTTPS는 **기본적으로 443포트**를 사용하지만 서버와 웹 브라우저가 이 과정을 자동으로 처리하여 사용자 경험을 개선한다.

`http://` 혹은 `https://`를 입력하는 경우 해당 프로토콜의 기본 포트로 접속을 시도하게 된다.

**HSTS (HTTP Strict Transport Security)** 를 통해서 특정 도메인에 대해 HTTPS만 사용하라는 정책을 전달할 수 있다. 예를 들어 사용자가 `http://naver.com`을 입력하더라도 서버가 HSTS 정책을 전달한 적이 있다면 브라우저는 우선적으로 443 포트, `https://naver.com`로 연결을 시도한다.

또는 인기있는 웹사이트나 HTTPS 지원 웹사이트에 접속했던 기록이 있는 경우 브라우저에 내장된 목록(HSTS Preload List)을 통해 자동으로 HTTPS 연결을 시도한다.

### Q. TLS 연결 시 서버가 보내준 CA 인증서가 올바른 인증서인지 확인하는 절차

TLS 연결 시, 클라이언트가 서버가 보내준 **CA 인증서**가 올바른 인증서인지 확인하는 과정은 **인증서 체인(Certificate Chain)** 과 **신뢰할 수 있는 루트 인증서(Trust Store)** 를 사용하여 이루어진다. 

이 과정에서 클라이언트는 서버가 제시한 인증서를 **신뢰할 수 있는 루트 인증 기관(CA)** 이 발급한 것인지, 그리고 해당 인증서가 **위조되지 않았는지**를 검증하게 된다.

1. 서버로부터 **인증서 체인**을 수신하고 검토
2. **인증서 체인**이 클라이언트의 **Trust Store**에 포함된 **루트 인증서**로 이어지는지 확인
3. **인증서 서명**이 올바른지 검증
4. **유효 기간**이 맞는지 확인
5. **인증서의 도메인**이 클라이언트가 접속하려는 도메인과 일치하는지 확인

>[!note]- 인증서 검증 과정의 세부 절차
>
>
> 1. **서버의 인증서 수신**
 >	- 서버는 클라이언트가 연결을 시도할 때 **서버 인증서**를 클라이언트에 전송합니다. 이 서버 인증서는 **CA(인증 기관)** 에 의해 발급된 것이며, 보통 인증서 체인(Intermediate CA 인증서 포함)을 함께 전달합니다.
> 2. **인증서 체인 확인**
  >	- 클라이언트는 서버가 제공한 **인증서 체인**을 분석합니다. 인증서 체인은 **서버 인증서**와 **중간 인증서(Intermediate CA)** 로 구성되며, 최종적으로 **루트 인증서(Root CA)** 까지 연결됩니다.
>	- 클라이언트는 서버의 인증서가 중간 인증서에 의해 서명되었는지 확인하고, 그 중간 인증서가 더 상위의 중간 인증서 또는 최종적으로 **루트 인증서**에 의해 서명되었는지 순차적으로 검증합니다.
> 3. **루트 인증서 확인 (Trust Store)** 
>	- 클라이언트는 **루트 인증서**를 확인하여, 해당 루트 인증서가 클라이언트의 **신뢰할 수 있는 인증서 저장소(Trust Store)** 에 포함되어 있는지 검사합니다.
>	- **Trust Store**는 운영 체제 또는 브라우저에 내장되어 있는 신뢰할 수 있는 CA 목록입니다. 여기에는 여러 **공인된 루트 인증서**가 포함되어 있으며, 클라이언트는 이 목록과 서버의 인증서 체인을 비교하여 유효성을 확인합니다.
>	- 만약 클라이언트의 Trust Store에 있는 루트 인증서와 서버의 인증서 체인이 일치하면, 클라이언트는 서버의 인증서를 **신뢰할 수 있는 것으로** 간주합니다.
> 4. **인증서 유효성 검증**
>	- 클라이언트는 서버의 인증서가 **유효 기간** 내에 있는지 확인합니다. 만약 유효 기간이 지났거나 아직 유효하지 않은 경우, 인증서 검증에 실패합니다.
>	- 또한, 클라이언트는 인증서의 **서명**을 검증합니다. 서버의 인증서가 중간 CA 또는 루트 CA의 **비밀키**로 서명된 것을 확인하기 위해, 클라이언트는 인증서의 **서명 알고리즘**과 **공개키**를 사용하여 서명이 올바른지 검증합니다.
> 5. **인증서 도메인 일치 여부 확인** 
>	- 클라이언트는 서버 인증서에 포함된 **공통 이름(CN, Common Name)** 또는 **주체 대체 이름(SAN, Subject Alternative Name)** 이 클라이언트가 접속하려는 도메인과 일치하는지 확인합니다.
>	- 예를 들어, 클라이언트가 `https://example.com`에 접속할 때 서버가 제공한 인증서의 CN이 `example.com`이거나 SAN 필드에 `example.com`이 포함되어 있어야 합니다. 도메인이 일치하지 않으면 인증서 검증에 실패합니다.

## 적용하기

>[!warning] 소유중인 도메인이 없어 실제 프로젝트에 적용해보지 못함

인증서를 발급받는 과정이 필요한데, 아래는 Certbot을 이용하여 Let's Encrypt의 무료 인증서를 발급받는 과정이다.

```bash
sudo certbot certonly --standalone -d yourdomain.com
```

발급 된 인증서는 보통 `/etc/letsencrypt/live/yourdomain.com/`에 저장된다.

- **Fullchain 인증서**: `/etc/letsencrypt/live/yourdomain.com/fullchain.pem`
- **Private Key**: `/etc/letsencrypt/live/yourdomain.com/privkey.pem`

스프링 부트의 내장 Tomcat 서버에서 HTTPS를 설정하려면, 인증서를 **PKCS12** 형식으로 변환해야 한다. `openssl` 명령어를 사용하여 변환한다.

```bash
sudo openssl pkcs12 -export -in /etc/letsencrypt/live/yourdomain.com/fullchain.pem \
                    -inkey /etc/letsencrypt/live/yourdomain.com/privkey.pem \
                    -out /etc/letsencrypt/live/yourdomain.com/keystore.p12 \
                    -name tomcat \
                    -CAfile /etc/letsencrypt/live/yourdomain.com/chain.pem \
                    -caname root
```

- `-in`: 인증서 파일 (fullchain.pem)
- `-inkey`: 개인 키 파일 (privkey.pem)
- `-out`: 생성할 PKCS12 키스토어 파일 경로
- `-name`: 키의 이름 (예: `tomcat`)
- `-CAfile`과 `-caname`: CA 체인 정보

이후 스프링 부트의 프로퍼티 파일을 수정한다.

```yml
server:  
  port: 443  
  ssl:  
    key-store: classpath:keystore.p12  
    key-store-password: your_password  
    key-store-type: PKCS12  
    key-alias: tomcat
```

Let's Encrypt 인증서는 **90일**의 유효기간을 가지므로, 자동으로 갱신되도록 설정해야 한다.
Certbot은 이를 자동화할 수 있는 기능을 제공한다.

- 자동 갱신 테스트 명령어:

```bash
sudo certbot renew --dry-run
```
    
- Certbot은 기본적으로 **cron job**이나 **systemd timer**를 설정하여 인증서를 주기적으로 갱신하며 이 설정은 Certbot 설치 시 자동으로 적용된다. 인증서 갱신 후에는 **서버를 자동으로 재시작**하거나 **스프링 부트 애플리케이션**을 재배포하는 스크립트를 추가로 설정하는 것이 좋다.

## 참조

- [Mozilla - Evolution of HTTP](https://developer.mozilla.org/ko/docs/Web/HTTP/Evolution_of_HTTP)
- [HTTP-통신-프로토콜 - velog](https://velog.io/@fnrkp089/HTTP%ED%86%B5%EC%8B%A0-%ED%86%B5%EC%8B%A0-%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C)
- [네트워크 이해하기 TCP - 티스토리](https://mindnet.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-22%ED%8E%B8-TCP-3-WayHandshake-4-WayHandshake)
	- 각 특장점 및 기술에 대해 좀 더 상세하게 작성되어 있음.
- ChatGPT 질의
	- 하이퍼 텍스트 프로토콜인데 다른 멀티미디어 데이터 교환이 가능해진 이유
	- 단순 요청-응답 모델과 무상태성, 단순성이 필요한 프토콜이 등장하게 된 배경
	- HTTP 프로토콜은 기본적으로 Stateless하게 설계되었지만 현 시점에서는 사실상 클라이언트가 얼마든지 현재 자신의 State를 알려줄 수 있는 방법이 있으므로 Stateless하다고 볼 수 없지 않는가?
	- 무상태성을 가지는 단순 요청-응답 모델에서 웹소켓과 같은 실시간 양방향 통신이 가능한 이유
	- 기존 HTTP/1.1을 사용하는 웹앱에서 HTTP/2나 HTTP/3를 적용하는 방법
	- HTTP에서 HTTPS가 필요했던 이유
		- 등장 배경
		- HTTPS가 1995년, HTTP/1.1이 1996년에 개발되었는데 HTTP 프로토콜이 직접적으로 암호화를 지원하기 시작한건 HTTP/3(2020년)인데 이들이 별개의 개념인 이유
	- HTTPS의 통신법
	- 세션키를 사용해 서버가 대칭키를 설정하는데 클라이언트가 그 대칭키를 몰라도 되는 이유
	- 클라이언트가 제안한 TLS 버전이나 암호화 방식 중 서버가 채택할 수 있는게 없다면?
	- 세션키가 그대로 서버-클라이언트간의 대칭키로 사용된다는건데, 그럼 세션 키가 탈취당하는 경우는?
	- 브라우저에서 특별히 HTTP 80포트나 HTTPS 443포트를 명시하지 않더라도 자동 전환이 되는 이유는?
	- TLS 연결 시 서버가 보내준 CA 인증서가 올바른 인증서인지 확인하는 절차
	- 인증서와 인증서 체인에 포함된 내역
