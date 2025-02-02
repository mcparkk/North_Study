## RESTful 개념과 RESTful API

## 1. REST란?
REST(Representational State Transfer)의 약자로, 자원을 이름으로 구분하여 해당 자원의 상태를 주고받는 모든 것을 의미합니다.

즉, REST란
- HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고,
- HTTP Method(POST, GET, PUT, DELETE, PATCH 등)를 통해
- 해당 자원(URI)에 대한 CRUD Operation을 적용하는 것을 의미한다.

### CRUD Operation이란?
CRUD는 대부분의 컴퓨터 소프트웨어가 가지는 기본적인 데이터 처리 기능인 Create(생성), Read(읽기), Update(갱신), Delete(삭제)를 묶어서 일컫는 말입니다.
REST에서의 CRUD Operation 동작 예시는 다음과 같습니다.

- **Create** : 데이터 생성 (POST)
- **Read** : 데이터 조회 (GET)
- **Update** : 데이터 수정 (PUT, PATCH)
- **Delete** : 데이터 삭제 (DELETE)

### REST 구성 요소
REST는 다음과 같은 3가지로 구성이 되어 있습니다.

1. **자원(Resource)** : HTTP URI
2. **자원에 대한 행위(Verb)** : HTTP Method
3. **자원에 대한 행위의 내용 (Representations)** : HTTP Message Payload

### REST의 주요 원칙
1. **클라이언트-서버(Client-Server)**: 클라이언트와 서버는 분리되어 있으며, 클라이언트는 요청을 보내고 서버는 응답을 반환한다.
2. **무상태성(Stateless)**: 각 요청은 독립적이며, 서버는 클라이언트의 상태를 유지하지 않는다.
3. **캐시 가능(Cacheable)**: HTTP 프로토콜의 캐시 기능을 활용하여 성능을 향상시킬 수 있다.
4. **계층화(Layered System)**: 중간 서버(프록시, 게이트웨이 등)를 두어 확장성을 높일 수 있다.
5. **일관된 인터페이스(Uniform Interface)**: 자원(Resource)에 대한 접근을 일정한 인터페이스로 제공한다.
6. **코드 온 디맨드(Optional)**: 서버에서 클라이언트로 실행 가능한 코드(JavaScript 등)를 전달할 수 있다.

## 2. RESTful API란?
RESTful API는 REST 원칙을 따르는 API(Application Programming Interface)이다. 즉, 웹에서 REST 아키텍처 스타일을 기반으로 클라이언트와 서버 간의 데이터를 주고받는 방식으로 동작한다.

### RESTful API의 특징

- **자원을 URI(Uniform Resource Identifier)로 표현**: 예를 들어, `https://api.example.com/users`는 `users`라는 자원을 의미한다.
- **HTTP 메서드를 활용**:
   - `GET`: 자원 조회
   - `POST`: 자원 생성
   - `PUT`: 자원 전체 수정 (멱등성 보장)
   - `PATCH`: 자원 일부 수정 (멱등성이 보장될 수도, 안될 수도 있음)
   - `DELETE`: 자원 삭제 (보통 멱등성을 가짐)
- **JSON 또는 XML 기반의 데이터 교환**: 일반적으로 JSON을 사용한다.
- **일관된 응답 구조**: RESTful API는 예측 가능한 구조를 유지해야 한다.
- **멱등성** : 동일한 연산을 여러 번 수행해도 결과가 달라지지 않는 성질을 말한다.(sql Update)

### PUT과 PATCH의 차이점
1. **PUT (전체 업데이트, 멱등성 보장)**
   - 기존 데이터를 새로운 데이터로 완전히 덮어쓴다.
   - 동일한 요청을 여러 번 보내도 결과가 동일하다.
   - 일반적으로 모든 필드를 포함하여 요청해야 한다.

   **예시 (사용자 정보 전체 업데이트)**
   ```http
   PUT /users/1
   Content-Type: application/json
   ```
   요청 바디:
   ```json
   { "name": "Alice Updated", "email": "alice@example.com" }
   ```

2. **PATCH (부분 업데이트, 멱등성이 보장될 수도 있고, 아닐 수도 있음)**
   - 특정 필드만 변경할 수 있다.
   - 멱등성이 보장되는 경우와 보장되지 않는 경우가 있음.

   **멱등성이 보장되는 예시:**
   ```http
   PATCH /users/1
   Content-Type: application/json
   ```
   요청 바디:
   ```json
   { "email": "alice_new@example.com" }
   ```
   - 여러 번 요청해도 `email` 값이 동일하게 유지됨 → **멱등성 O**

   **멱등성이 보장되지 않는 예시:**
   ```http
   PATCH /users/1
   Content-Type: application/json
   ```
   요청 바디:
   ```json
   { "last_login": "2025-02-02T12:34:56Z" }
   ```
   - 요청할 때마다 `last_login` 값이 갱신됨 → **멱등성 X**

## 3. RESTful API의 장점
- **확장성이 뛰어남**: 클라이언트와 서버가 분리되어 있어 유연하게 확장할 수 있다.
- **가독성이 높음**: 일관된 URI 구조를 사용하여 가독성이 뛰어나다.
- **다양한 클라이언트에서 사용 가능**: 웹, 모바일 앱, IoT 등 다양한 환경에서 활용 가능하다.
- **표준 HTTP 프로토콜을 사용하여 구현이 간단**

## 4. RESTful API의 한계
- **오버페칭(Over-fetching) 문제**: 필요한 데이터보다 더 많은 데이터를 반환할 수 있다.
- **언더페칭(Under-fetching) 문제**: 필요한 데이터가 여러 엔드포인트에서 제공될 경우 여러 번의 요청이 필요할 수 있다.
- **보안 문제**: 무상태성이므로 인증과 보안에 대한 추가적인 조치가 필요하다.

## 5. RESTful API 설계 사례
1. **명확한 URI 사용**: 동작을 URI가 아닌 HTTP 메서드로 표현해야 한다.
    - ❌ `GET /getUser` → ✅ `GET /users/{id}`
    - ❌ `POST /createUser` → ✅ `POST /users`
2. **일관된 응답 코드 사용**:
    - `200 OK`: 요청 성공
    - `201 Created`: 새로운 리소스 생성
    - `400 Bad Request`: 잘못된 요청
    - `404 Not Found`: 리소스를 찾을 수 없음
    - `500 Internal Server Error`: 서버 내부 오류
3. **필요한 경우에만 응답 데이터 포함**: 불필요한 데이터 전송을 최소화해야 한다.
4. **보안 고려**: JWT, OAuth 등의 인증 방식을 활용하여 보안을 강화한다.

## 6. RESTful API와 기타 아키텍처 비교
| 특징         | RESTful API | GraphQL | gRPC |
|-------------|------------|---------|------|
| 데이터 요청 방식 | 여러 엔드포인트에서 요청 | 단일 엔드포인트에서 요청 | 단일 엔드포인트에서 요청 |
| 응답 데이터   | 정해진 구조의 응답 | 클라이언트가 원하는 데이터만 | 바이너리 데이터 송수신 |
| 성능         | 중간 | 높음 | 매우 높음 |
| 사용 사례    | 웹 API, 일반적인 서비스 | 복잡한 데이터 요구사항 | 마이크로서비스, 고성능 API |

## 결론
RESTful API는 웹 서비스 설계를 위한 강력하고 직관적인 방법이다. HTTP 프로토콜을 기반으로 하며, 클라이언트-서버 구조, 무상태성 등의 원칙을 따른다. 하지만 오버페칭과 보안 문제 등의 단점이 있을 수 있어, 필요에 따라 GraphQL이나 gRPC 같은 대안을 고려할 수 있다.


