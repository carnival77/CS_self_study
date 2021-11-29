### REST와 RESTful의 개념

-   REST란
    -   REST의 정의
        -   "Representational State Transfer(대표적인 상태 전달)"의 약자
        -   월드 와이드 웹(www)과 같은 분산 하이퍼미디어 시스템을 위한 소프트웨어 개발 아키텍처의 한 형식
            -   REST는 기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일이다.
            -   REST는 네트워크 상에서 Client와 Server 사이의 통신 방식 중 하나이다.
    -   REST의 구체적인 개념
        -   **HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고, HTTP Method(Post, Get, Put, Delete)를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것을 의미한다.**
            -   즉, REST는 자원 기반의 구조(ROA, Resource Oriented Architecture) 설계의 중심에 Resource가 있고 HTTP Method를 통해 Resource를 처리하도록 설계된 아키텍쳐를 의미한다.
            -   웹 사이트의 이미지, 텍스트, DB 내용 등의 모든 자원에 고유한 ID인 HTTP URI를 부여한다.
    -   REST 장단점
        -   장점
            -   여러 가지 서비스 디자인에서 생길 수 있는 문제를 최소화해준다.
            -   Hypermedia API의 기본을 충실히 지키면서 범용성을 보장한다.
            -   HTTP 프로토콜의 표준을 최대한 활용하여 여러 추가적인 장점을 함께 가져갈 수 있게 해준다.
        -   단점
            -   브라우저를 통해 테스트할 일이 많은 서비스라면 쉽게 고칠 수 있는 URL보다 Header 값이 왠지 더 어렵게 느껴진다.
            -   구형 브라우저가 아직 제대로 지원해주지 못하는 부분이 존재한다.
                -   PUT, DELETE를 사용하지 못하는 점
                -   pushState를 지원하지 않는 점
    -   REST가 필요한 이유
        -   '애플리케이션 분리 및 통합'
        -   '다양한 클라이언트의 등장'
        -   즉, 최근의 서버 프로그램은 다양한 브라우저와 안드로이폰, 아이폰과 같은 모바일 디바이스에서도 통신을 할 수 있어야 한다.
    -   REST 구성 요소
        1.  자원(Resource): URI
            -   모든 자원에 고유한 ID가 존재하고, 이 자원은 Server에 존재한다.
            -   자원을 구별하는 ID는 '/groups/:group_id'와 같은 HTTP  **URI**  다.
            -   Client는 URI를 이용해서 자원을 지정하고 해당 자원의 상태(정보)에 대한 조작을 Server에 요청한다.
        2.  행위(Verb): HTTP Method
            -   HTTP 프로토콜의 Method를 사용한다.
            -   HTTP 프로토콜은  **GET, POST, PUT, DELETE, HEAD**  와 같은 메서드를 제공한다.
        3.  표현(Representation of Resource)
            -   Client가 자원의 상태(정보)에 대한 조작을 요청하면 Server는 이에 적절한 응답(Representation)을 보낸다.
            -   REST에서 하나의 자원은  **JSON, XML, TEXT, RSS**  등 여러 형태의 Representation으로 나타내어 질 수 있다.
            -   JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적이다.
    -   REST 특징
        1.  Server-Client(서버-클라이언트 구조)
        2.  Stateless(무상태)
        3.  Cacheable(캐시 처리 가능)
        4.  Layered System(계층화)
        5.  Code-On-Demand(optional)
        6.  Uniform Interface(인터페이스 일관성)
-   REST API
    -   REST API의 정의
        -   REST 기반으로 서비스 API를 구현한 것
        -   최근 OpenAPI(누구나 사용할 수 있도록 공개된 API: 구글 맵, 공공 데이터 등), 마이크로 서비스(하나의 큰 애플리케이션을 여러 개의 작은 애플리케이션으로 쪼개어 변경과 조합이 가능하도록 만든 아키텍처) 등을 제공하는 업체 대부분은 REST API를 제공한다.
    -   REST API의 특징
        -   사내 시스템들도 REST 기반으로 시스템을 분산해 확장성과 재사용성을 높여 유지보수 및 운용을 편리하게 할 수 있다.
        -   REST는 HTTP 표준을 기반으로 구현하므로, HTTP를 지원하는 프로그램 언어로 클라이언트, 서버를 구현할 수 있다.
        -   즉, REST API를 제작하면 델파이 클라이언트 뿐 아니라, 자바, C#, 웹 등을 이용해 클라이언트를 제작할 수 있다.
    -   REST API 설계  **기본 규칙**
        1.  URI는 정보의 자원을 표현해야 한다.
            -   resource는 동사보다는 명사를 사용한다.
            -   resource는 영어 소문자 복수형을 사용하여 표현한다.
            -   Ex)  `GET /Member/1`  ->  `GET /members/1`
        2.  자원에 대한 행위는 HTTP Method(GET, PUT, POST, DELETE 등)로 표현한다.
            -   URI에 HTTP Method가 들어가면 안된다.
            -   Ex)  `GET /members/delete/1`  ->  `DELETE /members/1`
            -   URI에 행위에 대한 동사 표현이 들어가면 안된다.
            -   Ex)  `GET /members/show/1`  ->  `GET /members/1`
            -   Ex)  `GET /members/insert/2`  ->  `POST /members/2`
    -   REST API 설계 규칙
        1.  슬래시 구분자(/ )는 계층 관계를 나타내는데 사용한다.
            -   Ex)  `http://restapi.example.com/houses/apartments`
        2.  URI 마지막 문자로 슬래시(/ )를 포함하지 않는다.
            -   URI에 포함되는 모든 글자는 리소스의 유일한 식별자로 사용되어야 하며 URI가 다르다는 것은 리소스가 다르다는 것이고, 역으로 리소스가 다르면 URI도 달라져야 한다.
            -   REST API는 분명한 URI를 만들어 통신을 해야 하기 때문에 혼동을 주지 않도록 URI 경로의 마지막에는 슬래시(/)를 사용하지 않는다.
            -   Ex)  `http://restapi.example.com/houses/apartments/ (X)`
        3.  하이픈(- )은 URI 가독성을 높이는데 사용
            -   불가피하게 긴 URI경로를 사용하게 된다면 하이픈을 사용해 가독성을 높인다.
        4.  밑줄(_ )은 URI에 사용하지 않는다.
            -   밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려지기도 하므로 가독성을 위해 밑줄은 사용하지 않는다.
        5.  URI 경로에는 소문자가 적합하다.
            -   URI 경로에 대문자 사용은 피하도록 한다.
            -   RFC 3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 규정하기 때문
        6.  파일확장자는 URI에 포함하지 않는다.
            -   REST API에서는 메시지 바디 내용의 포맷을 나타내기 위한 파일 확장자를 URI 안에 포함시키지 않는다.
            -   Accept header를 사용한다.
            -   Ex)  `http://restapi.example.com/members/soccer/345/photo.jpg (X)`
            -   Ex)  `GET / members/soccer/345/photo HTTP/1.1 Host: restapi.example.com Accept: image/jpg (O)`
        7.  리소스 간에는 연관 관계가 있는 경우
            -   /리소스명/리소스 ID/관계가 있는 다른 리소스명
            -   Ex)  `GET : /users/{userid}/devices (일반적으로 소유 ‘has’의 관계를 표현할 때)`
        8.  :id는 하나의 특정 resource를 나타내는 고유값
            -   Ex) student를 생성하는 route: POST /students
            -   Ex) id=12인 student를 삭제하는 route: DELETE /students/12
-   RESTful
    -   RESTful의 개념
        -   RESTful은 일반적으로 REST라는 아키텍처를 구현하는 웹 서비스를 나타내기 위해 사용되는 용어이다.
            -   즉, REST 원리를 따르는 시스템은 RESTful이란 용어로 지칭된다.
        -   RESTful은 REST를 REST답게 쓰기 위한 방법으로, 누군가가 공식적으로 발표한 것이 아니다.
    -   RESTful의 목적
        -   이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것
        -   RESTful API를 구현하는 근본적인 목적이 퍼포먼스 향상에 있는게 아니라, 일관적인 컨벤션을 통한 API의 이해도 및 호환성을 높이는게 주 동기이니, 퍼포먼스가 중요한 상황에서는 굳이 RESTful API를 구현하실 필요는 없습니다.
    -   RESTful 하지 못한 경우
        -   Ex1) CRUD 기능을 모두 POST로만 처리하는 API
        -   Ex2) route에 resource, id 외의 정보가 들어가는 경우(/students/updateName)

> ⏫[Top](https://github.com/carnival77/tech-interview/blob/master/contents/network.md#2-network)  ↩️[Back](https://github.com/Do-Hee/tech-interview#2-network)  ℹ️[Home](https://github.com/Do-Hee/tech-interview#tech-interview)
> 
> -   [https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html](https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html)
> -   [https://www.a-mean-blog.com/ko/blog/%ED%86%A0%EB%A7%89%EA%B8%80/_/REST%EC%99%80-RESTful-API](https://www.a-mean-blog.com/ko/blog/%ED%86%A0%EB%A7%89%EA%B8%80/_/REST%EC%99%80-RESTful-API)
> -   [http://mygumi.tistory.com/55](http://mygumi.tistory.com/55)
> -   [https://brainbackdoor.tistory.com/53](https://brainbackdoor.tistory.com/53)
> -   [http://tech.devgear.co.kr/delphi_news/433404](http://tech.devgear.co.kr/delphi_news/433404)
> -   [https://meetup.toast.com/posts/92](https://meetup.toast.com/posts/92)
> -   [https://spoqa.github.io/2012/02/27/rest-introduction.html](https://spoqa.github.io/2012/02/27/rest-introduction.html)