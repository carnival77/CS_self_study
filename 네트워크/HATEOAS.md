# **HATEOAS (Hypermedia as the Engine of Application State)**

HATEOAS는 **REST API의 중요한 원칙** 중 하나로, 클라이언트가 서버와 상호작용을 할 때 필요한 모든 정보(리소스의 상태 및 가능한 동작)를 **응답 메시지 내에서 하이퍼미디어 형태로 제공**하는 것을 의미합니다.

---
- [**HATEOAS (Hypermedia as the Engine of Application State)**](#hateoas-hypermedia-as-the-engine-of-application-state)
  - [**특징**](#특징)
  - [**구조 예시**](#구조-예시)
  - [**장점**](#장점)
  - [**단점**](#단점)
  - [**요약**](#요약)
---

## **특징**

1. **동적 탐색**:
   - 클라이언트는 API 문서를 별도로 참조하지 않아도, 응답에 포함된 하이퍼링크를 따라가며 필요한 리소스에 접근하거나 작업을 수행할 수 있습니다.
2. **자체 설명적 메시지**:
   - API 응답이 리소스의 상태뿐만 아니라 다음에 수행할 수 있는 동작을 명시하여 클라이언트가 상태 전이를 이해할 수 있도록 합니다.
3. **REST의 완전한 구현**:
   - HATEOAS는 REST의 "Hypermedia Constraint"를 충족시키는 요소로, API 사용성을 개선하고 클라이언트와 서버의 결합도를 낮춥니다.

------

## **구조 예시**

**요청**:

```json
http
GET /users/1
```

**응답**:

```json
{
  "id": 1,
  "name": "John Doe",
  "email": "john.doe@example.com",
  "_links": {
    "self": { "href": "/users/1" },
    "update": { "href": "/users/1", "method": "PUT" },
    "delete": { "href": "/users/1", "method": "DELETE" },
    "posts": { "href": "/users/1/posts", "method": "GET" }
  }
}
```

- `_links` 속성은 클라이언트가 현재 리소스(`/users/1`)에 대해 수행할 수 있는 작업(수정, 삭제, 게시물 조회)을 명시적으로 제공.

------

## **장점**

- **클라이언트-서버 결합도 낮춤**: 클라이언트는 API 변경 시에도 응답 메시지의 링크를 따라가며 필요한 작업을 수행 가능.
- **동적 확장성**: 클라이언트는 서버의 상태를 하이퍼미디어를 통해 동적으로 탐색 가능.
- **API 문서 의존성 감소**: 클라이언트는 응답 메시지만으로도 상태 전이를 이해할 수 있음.

------

## **단점**

- 초기 설계가 복잡하며, 구현이 까다로울 수 있음.
- 클라이언트와 서버가 HATEOAS를 완전히 지원하도록 개발해야 함.

------

## **요약**

HATEOAS는 클라이언트가 서버의 리소스와 상호작용을 동적으로 수행할 수 있도록 **응답에 하이퍼미디어 링크를 포함하는 REST API 설계 원칙**으로, REST의 완전한 구현을 목표로 합니다.