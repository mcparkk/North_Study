# 쿠키와 세션

HTTP는 **무상태(stateless) 프로토콜**로, 클라이언트와 서버 간의 요청과 응답이 각각 독립적으로 처리된다.   
이를 보완하기 위해 **쿠키(Cookie)** 와 **세션(Session)** 그리고 **JWT** 가 사용된다.    
또한, 브라우저의 **로컬 스토리지(Local Storage)** 와 **세션 스토리지(Session Storage)** 는 상태 정보를 클라이언트 측에서 저장하는 또 다른 방법으로 사용된다.

---

## 쿠키(Cookie)

### 1. **쿠키란?**
쿠키는 클라이언트(사용자의 브라우저)에 저장되는 작은 데이터 조각으로, 사용자의 상태 정보를 클라이언트 측에 저장하고 이를 서버로 전달하는 방식으로 동작한다.

### 2. **쿠키의 사용 목적**
- 사용자의 상태 정보를 유지
- 클라이언트 측에서 데이터를 저장하여 서버 요청을 최소화

### 3. **쿠키의 종류**
1. 세션 쿠키 (Session Cookie)
- **정의**:
    - 세션 쿠키는 브라우저를 종료하면 자동으로 삭제되는 임시 쿠키.
    - 일반적으로 **브라우저를 닫으면 만료**되며, 서버에 세션 ID를 저장하고 클라이언트에서는 이 ID만을 저장.

- **사용 사례**:
    - **로그인 상태 유지**: 사용자가 로그인 상태로 브라우징하는 동안, 세션 쿠키를 사용하여 로그인 세션을 유지합니다.
    - **장바구니**: 쇼핑몰에서는 사용자가 사이트를 이동하는 동안 장바구니에 아이템을 추가할 때 세션 쿠키를 사용합니다. 브라우저를 닫으면 자동으로 장바구니 내용이 사라집니다.
    
- **특징**:
    - 브라우저를 닫을 때 삭제되므로 일시적인 데이터 저장에 적합합니다.
    - **보안**: 세션 쿠키는 서버에서 상태를 관리하고, 클라이언트는 세션 ID만 저장하므로 중요한 데이터를 서버에서 처리할 수 있다.

---

2. 영구 쿠키 (Persistent Cookie)
- **정의**:
    - 영구 쿠키는 만료 시간이 설정된 쿠키로, 설정된 기간 동안 브라우저를 닫고 다시 열어도 계속 유지됩니다.
    - 만료 시간이 지나면 자동으로 삭제됩니다.

- **사용 사례**:
    - **자동 로그인**: 사용자가 로그인 후 브라우저를 닫고 다시 열었을 때 자동으로 로그인 상태를 유지할 수 있게 해줍니다. 로그인 정보나 인증 토큰을 영구 쿠키에 저장하여 이를 사용한다.
    - **사용자 설정 저장**: 예를 들어, 언어 설정이나 테마 설정을 영구 쿠키에 저장하여 사용자가 다시 방문할 때 동일한 설정을 적용할 수 있다.

- **특징**:
    - **만료 시간**이 설정되어 있기 때문에, 브라우저를 종료하고 다시 시작해도 유지된다.
    - 장기간 동안 데이터를 저장해야 하는 경우에 유용하다.

---

3. 보안 쿠키 (Secure Cookie)
- **정의**:
    - 보안 쿠키는 **HTTPS 연결**에서만 전송되는 쿠키입니다. 즉, HTTP가 아닌 **암호화된 HTTPS 프로토콜**을 사용할 때만 전송된다.

- **사용 사례**:
    - **민감한 정보**(예: 로그인 토큰, 인증 토큰) 전송 시 보안 쿠키를 사용하여 데이터가 암호화된 채로 안전하게 전송되도록 보장한다.
    - **온라인 뱅킹**과 같은 보안이 중요한 사이트에서는 로그인 세션 및 인증 데이터를 보안 쿠키를 통해 보호한다.

- **특징**:
    - **HTTPS** 연결을 사용할 때만 쿠키가 전송되므로, HTTP 연결을 사용할 때는 해당 쿠키가 전송되지 않는다.
    - 보안이 중요한 정보가 포함된 쿠키에 적용하여, 중간자 공격(MITM)으로부터 보호한다.

---

4. HttpOnly 쿠키
- **정의**:
    - `HttpOnly` 속성은 **자바스크립트**가 해당 쿠키에 접근하지 못하도록 설정하는 보안 속성이다.
    - 이 속성이 설정된 쿠키는 **자바스크립트**에서 `document.cookie`를 사용해 접근할 수 없으며, **HTTP 요청**을 통해서만 서버로 전송된다.

- **사용 사례**:
    - **XSS(크로스 사이트 스크립팅) 공격 방지**: 자바스크립트를 통한 쿠키 탈취를 방지하는 데 사용된다. 예를 들어, 로그인 세션 정보를 `HttpOnly` 쿠키에 저장하여 XSS 공격자가 해당 쿠키를 읽지 못하도록 보호할 수 있다.
    - **세션 관리**: 로그인 세션을 `HttpOnly` 쿠키에 저장하여 자바스크립트 코드가 이를 액세스하지 못하도록 하고, 보안을 강화한다.

- **특징**:
    - **자바스크립트에서 접근 불가**: `document.cookie`로 접근할 수 없고, 서버에서만 쿠키를 읽고 쓸 수 있다.
    - **보안 강화**: XSS 공격을 예방하는 데 중요한 역할을 한다.

---

5. SameSite 쿠키
- **정의**:
    - `SameSite` 속성은 **크로스 사이트 요청 위조(CSRF)** 공격을 방지하는 데 사용된다. 이 속성은 쿠키가 **같은 사이트**에서만 전송되도록 제한할 수 있다.
    - `SameSite` 속성은 세 가지 옵션을 가질 수 있습니다:
        - **Strict**: 쿠키는 **같은 사이트**에서만 전송된다. 다른 사이트에서 이 쿠키를 사용할 수 없다.
        - **Lax**: `Strict`보다는 덜 제한적이며, 사용자가 링크를 클릭할 때 같은 사이트에서 쿠키를 전송합니다. 단, 외부 사이트의 `POST` 요청 등에서는 쿠키가 전송되지 않는다.
        - **None**: 크로스 사이트에서 쿠키가 전송될 수 있도록 허용한다. 그러나 `Secure` 속성과 함께 사용해야 하며, HTTPS 연결에서만 작동한다.

- **사용 사례**:
    - **CSRF 공격 방지**: `SameSite=Strict`나 `SameSite=Lax`를 사용하여 외부 사이트에서 민감한 데이터를 다루는 요청을 막을 수 있다.
    - **외부 사이트 인증**: 외부 서비스(예: 소셜 로그인)가 사용할 때 `SameSite=None`을 설정하여 외부 요청에서도 쿠키를 전달할 수 있도록 한다.

- **특징**:
    - CSRF 공격을 예방하는 데 유용하며, 특히 인증 관련 쿠키에 적용된다.
    - `Strict`와 `Lax`는 **같은 사이트**에서만 쿠키를 보내므로 보안을 강화하는 데 사용되고, `None`은 외부 사이트와의 인증을 지원하는 데 사용된다.

---

### **각 쿠키의 적용 사례**

- **세션 쿠키**: 로그인 상태 관리, 장바구니 유지 등 일시적인 데이터 저장.
- **영구 쿠키**: 자동 로그인, 사용자 설정 저장 등 장기적인 데이터 저장.
- **보안 쿠키**: 로그인 토큰, 인증 정보와 같이 민감한 정보를 안전하게 전송.
- **HttpOnly 쿠키**: XSS 공격 방지를 위해 로그인 세션이나 인증 정보 저장.
- **SameSite 쿠키**: CSRF 공격 방지 및 외부 사이트와의 안전한 쿠키 전달 관리.

---

## 세션(Session)

### 1. **세션이란?**
세션은 서버에서 사용자 상태를 관리하는 메커니즘으로, 클라이언트와의 상호작용을 통해 생성되며, 고유한 **세션 ID**를 통해 클라이언트를 식별한다.

### 2. **세션의 동작 원리**
1. 클라이언트가 서버에 요청을 보낸다.
2. 서버는 고유한 **세션 ID**를 생성하고 이를 클라이언트에게 쿠키로 전달한다.
3. 클라이언트는 이후 요청마다 이 **세션 ID**를 포함하여 서버에 보낸다.
4. 서버는 세션 ID를 확인하고 사용자 상태를 유지한다.

### 3. **세션의 특징**
- **저장 위치**: 서버에 저장
- **보안성**: 데이터가 서버에 저장되므로 보안이 높음
- **단점**: 많은 사용자가 접속할 경우, 서버 메모리 사용량 증가

---

## JWT (JSON Web Token)
### 1. **JWT란?**:
 JSON 형식으로 인코딩된 **자기 포함형 토큰**으로, 사용자 인증 및 권한 부여에 사용된다.

### 2. **JWT의 구조**:
  - **Header:** 토큰의 형식 (JWT)과 서명 알고리즘 (예: HS256) 등을 나타냅니다.
  - **Payload:** 사용자 정보 (예: 사용자 ID, 이름, 권한 등)를 JSON 형태로 담고 있습니다.
  - **Signature:** Header와 Payload를 연결하여 생성한 서명 값으로, 토큰의 무결성을 보장합니다.   

JWT의 구조도:
```json
{
  "header": {
    "typ": "JWT",
    "alg": "HS256"
  },
  "payload": {
    "sub": "1234567890",
    "name": "John Doe",
    "admin": true,
    "exp": 1516239022
  },
  "signature": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyLCJleHAiOjE1MTYyMzkwMjJ9.sMIIBVQyb21Faim4et0UW0h0hRhxoVjDjuYEPQjH9aqaW9"
}
```
### 3. **JWT의 장점**

* **자체 포함형:** 토큰 자체에 모든 정보가 포함되어 있어 서버에 추가적인 정보를 요청할 필요가 없다.
* **Stateless:** 서버에 세션을 유지할 필요가 없어 서버 부하를 줄일 수 있다.
* **확장성:** 다양한 정보를 추가하여 사용자 정의 토큰을 생성할 수 있다.
* **보안:** 서명을 통해 위변조를 방지하고, 필요에 따라 암호화하여 민감한 정보를 보호할 수 있다.

### 4. **JWT의 단점**

* **토큰 크기:** 토큰에 많은 정보를 담으면 크기가 커질 수 있다.
* **만료 시간:** 토큰의 유효 기간을 설정해야 하며, 만료 시간 관리가 필요하다.
* **토큰 탈취:** 토큰이 탈취되면 권한이 남용될 수 있다.
* **복잡성:** 구현하기 위해서는 암호화, 서명 등 다양한 기술을 이해해야 한다.

### 5. **JWT의 사용 사례**

* **로그인 인증:** 사용자 인증 정보를 토큰에 담아 전달하고, 이후 요청 시 토큰을 검증하여 인증을 수행한다.
* **API 인증:** API 호출 시 JWT를 헤더에 포함하여 인증을 수행한다.
* **권한 부여:** 사용자의 권한 정보를 토큰에 포함하여 권한을 부여한다.
* **단일 로그인:** 다양한 시스템 간에 JWT를 공유하여 단일 로그인을 구현할 수 있다.
---

## 브라우저 저장소: 로컬 스토리지와 세션 스토리지

### 1. **로컬 스토리지(Local Storage)**
- 클라이언트의 브라우저에 영구적으로 데이터를 저장하는 메커니즘
- 특징:
    - 데이터는 브라우저를 닫아도 유지된다.
    - 최대 저장 용량은 약 5~10MB로 쿠키보다 큼.
    - 서버와의 통신 없이 데이터 접근 가능
- 사용 사례:
    - 사용자 환경 설정 저장
    - 캐싱 데이터(예: 검색 기록)

### 2. **세션 스토리지(Session Storage)**
- 클라이언트의 브라우저에 데이터를 임시로 저장하는 메커니즘
- 특징:
    - 데이터는 브라우저 탭이 닫힐 때 삭제된다.
    - 각 브라우저 탭마다 독립적으로 저장
    - 최대 저장 용량은 로컬 스토리지와 유사
- 사용 사례:
    - 페이지 간 상태 정보 공유(단, 탭 내에서만)

### 3. **로컬 스토리지, 세션 스토리지 vs 쿠키**
| **특징**                 | **쿠키(Cookie)**            | **로컬 스토리지(Local Storage)** | **세션 스토리지(Session Storage)** |
|---------------------------|-----------------------------|-----------------------------------|-------------------------------------|
| **저장 위치**            | 클라이언트(브라우저)        | 클라이언트(브라우저)              | 클라이언트(브라우저)                |
| **만료 시점**            | 설정된 만료 시간           | 브라우저가 삭제될 때까지 유지     | 브라우저 탭을 닫으면 삭제           |
| **데이터 용량**          | 약 4KB                     | 약 5~10MB                         | 약 5~10MB                           |
| **데이터 전송**          | 매 요청마다 서버로 전송    | 서버로 자동 전송되지 않음         | 서버로 자동 전송되지 않음           |
| **보안**                 | 민감한 정보 저장에 부적합  | 보안에 민감한 데이터는 부적합     | 보안에 민감한 데이터는 부적합       |
| **사용 목적**            | 서버와의 상태 유지         | 클라이언트 상태 저장              | 일시적인 상태 저장(탭 한정)         |

---

## 쿠키, 세션, JWT의 차이점

| **특징**             | **쿠키**                        | **세션**                        | **JWT**                        |
|-----------------------|--------------------------------|--------------------------------|--------------------------------|
| **저장 위치**         | 클라이언트(브라우저)           | 서버                           | 클라이언트(쿠키, 로컬 스토리지 등) |
| **상태(State)**       | Stateless (단순 데이터 저장)  | Stateful (서버에서 상태 관리)  | Stateless (토큰 자체에 정보 포함) |
| **보안**             | 취약(HTTP-Only, Secure 설정 필요) | 비교적 안전(서버에만 저장)      | 비교적 안전(서명으로 위변조 방지) |
| **크기 제한**         | 약 4KB                        | 제한 없음                      | 일반적으로 1~2KB              |
| **속도**             | 빠름 (클라이언트에 저장)       | 느림 (서버 조회 필요)           | 빠름 (서버 조회 불필요)        |
| **만료 관리**         | 만료 시간 설정 가능            | 서버에서 관리                  | 토큰 자체에 만료 정보 포함     |
| **정보 저장**         | 세션 ID 등 간단한 정보         | 서버에 모든 사용자 정보 저장    | 사용자 정보 자체를 포함        |

---

## 쿠키, 세션, JWT의 관계

### 1. 쿠키와 세션의 관계
- 쿠키는 **세션 ID를 저장**하는 데 사용된다.
    - 사용자가 로그인하면 서버는 세션 ID를 생성하여 서버에 저장하고, 해당 ID를 클라이언트의 쿠키에 저장한다.
    - 이후 요청 시 브라우저는 쿠키에 저장된 세션 ID를 서버로 전송하고, 서버는 해당 ID로 세션 정보를 조회하여 사용자 인증 및 상태를 유지한다.
- 즉, **세션 방식을 사용하기 위해 쿠키는 필수적인 요소**이다.

---

### 2. JWT와 쿠키의 관계
- JWT는 클라이언트에 저장되며, 쿠키에 저장하는 것이 일반적이다.
    - 쿠키에 저장된 JWT는 HTTP 요청 시 자동으로 서버로 전달됩니다.
    - `HttpOnly`, `Secure`, `SameSite`와 같은 속성을 통해 보안을 강화할 수 있다.

---

### 3. JWT와 세션의 차이
- 세션은 상태를 **서버에서 관리**하지만, JWT는 **상태를 서버에 저장하지 않고 클라이언트에서 관리**한다.
- JWT는 서버가 상태를 유지하지 않아도 되므로, 분산 시스템(예: 마이크로서비스)에서 유리하다.

---

## 언제 무엇을 사용할까?

### 1. 쿠키 사용
- 간단한 데이터 저장.
- 로그인 상태 유지나 사용자 선호도 설정 저장에 적합.

### 2. 세션 사용
- 서버에서 사용자 상태를 관리해야 하는 경우.
- 고도의 보안이 요구되는 애플리케이션(예: 금융 서비스).

### 3. JWT 사용
- 서버가 상태를 저장하지 않아야 하는 경우(Stateless).
- 분산 시스템에서 인증 상태 공유가 필요한 경우.
- RESTful API와 클라이언트 간 인증.

---


## 참조
GPT 질의   
Gemini 질의   
[HTTP 쿠키](https://developer.mozilla.org/ko/docs/Web/HTTP/Cookies)
