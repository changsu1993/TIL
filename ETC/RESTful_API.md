# 1. REST API

**Representational State Transfer API** <br>

API(Application Programming Interface)는 응용 프로그램에서 사용할 수 있도록, 운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스를 말한다.

REST API는 REST 아키텍처 스타일의 디자인 원칙을 준수하는 API이다. <br>
최근 openAPI등을 제공하는 회사들은 대부분 REST API를 제공한다. <br><br>
**RESTful이란** <br>
RESTful은 일반적으로 REST라는 아키텍처를 구현하는 웹 서비스를 나타내기 위해 사용되는 용어이다. <br>
REST API를 제공하는 웹 서비스를 RESTful 하다고 할 수 있다. <br>
즉, REST 원리를 따르는 시스템은 RESTful이란 용어로 지칭된다. <br>

<br>

## REST 구성

**자원(Resource): URL**

- 자원에 고유한 ID 존재, 자원은 서버에 존재
- 자원을 구별하는 ID는 HTTP URI 이다.
- 클라이언트는 URI를 이용해 자원을 지정하고 자원의 상태에 대한 조작을 서버에 요청한다.

**행위(Verb): HTTP Method**

- HTTP 프로토콜의 Method를 사용하며, GET, POST, PUT, DELETE와 같은 메서드를 제공한다.<br>

**CRUD**<br>
POST - POST를 통해 해당 URI를 요청하면 리소스를 생성한다. <br>
GET - GET을 통해 해당 리소스를 조회한다. 리소스를 조회하고 해당 도큐먼트에 대한 자세한 정보를 가져온다. <br>
PUT - PUT을 통해 해당 리소스를 수정한다. <br>
DELETE - DELETE를 통해 리소스를 삭제한다.

**표현(Representations)**

- 클라이언트가 자원의 상태에 대한 조작을 요청하면 서버는 적절한 응답을 보낸다. <br>
- REST에서 하나의 자원은 XML,JSON,RSS 등 여러 형태의 Representation으로 나타낼 수 있다. <br>
- JSON 또는 XML을 통해 데이터를 주고 받는 것이 일반적이다.
  <br><br>

## REST 특징

**Uniform Interface(유니폼 인터페이스)** <br>
동일한 리소스에 대한 모든 API 요청은 동일하게 보여야 한다. REST API는 사용자의 이름이나 이메일 주소 등의 동일한 데이터 조각이 오직 하나의 URI에 속하는 것을 보장해야 한다. <br><br>

**Stateless(무상태성)** <br>
REST API는 Stateless이다. 작업을 위한 상태 정보(세션, 쿠키 정보)를 따로 저장하고 관리하지 않기 때문에 각 API 서버는 클라이언트의 요청만을 단순 처리한다. 그래서 자유도가 높아지고 서버에서 불필요한 정보를 관리하지 않음으로써 구현이 단순해진다. <br><br>

**Client-Server** <br>
REST API 디자인에서 클라이언트와 서버 애플리케이션은 독립적이여야 한다. <br>
클라이언트 - 사용자 인증 또는 컨텍스트(세션, 로그인 정보)등을 직접 관리하고 책임 <br>
REST 서버 - API를 제공하고 비즈니스 로직 처리 및 저장을 관리하고 책임
<br><br>

**Cacheable(캐시 처리 가능)** <br>
기존 웹 표준 HTTP 프로토콜을 그대로 사용하기 때문에, 웹에서 사용하는 기존 인프라를 그대로 활용 가능하다. 그래서 HTTP가 가진 캐싱 기능을 적용할 수 있다. HTTP 프로토콜 표준에서 사용하는 Last-Modified 태그나 E-Tag를 이용하면 캐싱 구현이 가능하다.
<br><br>

**Layered System(계층화 구조)** <br>
REST 서버는 다중 계층으로 구성될 수 있고 보안, 로드 밸러싱, 암호화, 사용자 인증 등을 추가해 구조상의 유연성을 둘 수 있다. <br>
PROXY, 게이트웨이 같은 네트워크 기반의 중간매체를 사용할 수 있다.
<br><br>

**Code-On-Demand(optional)** <br>
일반적으로 정적 리소스를 전송하지만, 특정한 경우에는 서버로부터 스크립트를 받아서 클아이언트에서 실행한다.
<br><br>

## REST API 디자인 가이드

- URI는 정보의 자원을 표현해야 한다.

**리소스명은** <br>
동사보다 명사로, 대문자보다 소문자를 사용한다. <br>
도큐먼트 이름으로 단수 명사를 사용해야 한다. <br>
컬렉션 이름으로는 복수 명사를 사용해야 한다. <br>
스토어 이름으로 복수 명사를 사용해야 한다. <br>

```javascript
GET / members / 1;
```

<br>

- 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE)로 표현한다.

**URI에** <br>
HTTP Method가 들어가면 안된다.

```javascript
GET /Members/delete/1 -> DELETE /members/1
```

행위에 대한 동사표현이 들어가면 안된다.

```javascript
GET /members/show/1 -> GET /members/1
GET /members/insert/2 -> POST /members/2
```

경로 부분 중 변하는 부분은 유일한 값으로 대체한다.

```javascript
ex) animal을 생성하는 route: POST /animal
ex) id = 1인 animal을 삭제하는 route: DELETE /animal/1
```

<br>

## REST API 설계 시 주의사항

**슬래시 구분자(/)는 계층 관계를 나타내는데 사용**

```javascript
http://restapi.example.com/houses/apartments
http://restapi.example.com/animals/mammals/whales
```

<br>

**URI 마지막 문자로 슬래시(/)를 포함하지 않는다.**
URI에 포함되는 모든 글자는 리소스의 유일한 식별자로 사용되어야 하며 URI가 다르다는 것은 리소스가 다르다는 것이고, 역으로 리소스가 다르면 URI도 달라져야 한다. <br>
REST API는 분명한 URI를 만들어 통신을 해야 하기 때문에 혼동을 주지 않도록 URI 경로의 마지막에는 슬래시(/)를 사용하지 않는다.

```javascript
http://restapi.example.com/houses/apartments/ (X)
http://restapi.example.com/houses/apartments  (0)
```

<br>

**하이픈(-)은 URI 가독성을 높이는데 사용** <br>
불가피하게 긴 URI경로를 사용하게 된다면 하이픈을 사용해 가독성을 높일 수 있다.
<br><br>

**밑줄(\_)은 URI에 사용하지 않는다.** <br>
밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려질 수도 있기 때문에 가독성을 위해 밑줄 대신 하이픈(-)을 사용하는 것이 좋다.
<br><br>

**URI 경로에는 소문자가 적합하다.** <br>
대소문자에 따라 다른 리소스로 인식하기 때문에 URI 경로에 대문자 사용은 피하도록 한다. <br>
RFC 3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 규정했다.
<br><br>

**파일확장자는 URI에 포함하지 않는다.** <br>
REST API에서는 메시지 바디 내용의 포맷을 나타내기 위한 파일 확장자를 URI 안에 포함시키지 않는다. Accept header를 사용한다.
<br><br>

**리소스 간의 관계를 표현하는 방법** <br>
REST 리소스 간에는 연관 관계가 있을 경우

```javascript
/리소스명/리소스 ID/관계가 있는 다른 리소스명

ex) GET : /users/{userid}/devices (일반적으로 소유 ‘has’의 관계를 표현할 때)
```

<br>

**자원을 표현하는 Collection과 Document** <br>

Document는 문서 또는 객체, Collection은 문서들의 집합, 객체들의 집합이다. <br>
Collection과 Document는 모두 리소스라고 표현할 수 있고, URI에 표현할 수 있다.

```javascript
http:// restapi.example.com/sports/soccer
Collection: sports , Document: soccer

http:// restapi.example.com/sports/soccer/players/13
Collection: sports, players
Document: soccer, 13
```

 <br>

**HTTP 응답 상태 코드** <br>
잘 설계된 REST API는 리소스에 대한 응답을 잘 내어주는 것까지 포함되어야 한다. 정확한 응답의 상태코드만으로도 많은 정보를 전달할 수 있기 때문에 응답의 상태코드 값을 명확히 돌려주는 것은 중요한 일이다. <br>

1xx : 전송 프로토콜 수준의 정보 교환 <br>
2xx : 클라이언트 요청이 성공적으로 수행 <br>
3xx : 요청을 완료하기 위해 클라이언트가 추가적인 행동을 취해야 함 <br>
4xx : 클라이언트의 요청이 부적절할 경우 <br>
5xx : 서버에 문제가 있을 경우
<br><br><br>

---

## References <br>

- https://spoqa.github.io/2012/02/27/rest-introduction.html

- https://www.redhat.com/ko/topics/api/what-is-a-rest-api

- https://ko.wikipedia.org/wiki/REST

- https://meetup.toast.com/posts/92

- https://brainbackdoor.tistory.com/53
