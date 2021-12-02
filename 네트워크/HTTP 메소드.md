<div  align="center">

<br />

<h1>HTTP의 GET과 POST 비교</h1>

<br />

</div>

  

## 목차

  

1.  [**REST**](#1)

2.  [**GET 방식**](#2)

3.  [**POST 방식**](#3)

4.  [**PUT 방식**](#4)

5.  [**DELETE 방식**](#5)

6.  [**비교**](#6)

  

<br />

  

<div  id="1"></div>

  

## REST(Representational State Transfer)

  

URI를 통해 자원을 표시하고, HTTP Method를 이용하여 해당 자원의 행위를 규정하여 그 결과를 받는 것을 말한다.

  

- 자원(Resource): URI

*해당 소프트웨어가 관리하는 모든 것 (ex 문서, 그림, 데이터, 소프트웨어 자체 등..)*

- 행위(Verb): HTTP Method

- 표현(Representations)

*자원을 표현하기 위한 이름 (ex 학생 정보가 자원이라면 'students'를 자원의 표현으로 정한다.)*

  

HTTP Method는 크게 GET, POST, PUT, DELETE가 대표적이며,

  

보통 CRUD에서 조회는 GET, 등록은 POST, 수정은 PUT, 삭제는 DELETE를 이용한다.

  

<img  src="https://user-images.githubusercontent.com/56222478/143454058-b936a794-eda1-40e2-97be-9d5899bad06b.png"  width="600px"  height="150px">

  
  

++ : [https://meetup.toast.com/posts/92](https://meetup.toast.com/posts/92)

  

### 추가 내용

- HTTP 전체 메소드 (8개)

	GET: 서버에 존재하는 데이터를 요청하는 것입니다. CRUD로 따지면 R입니다.

	POST: 서버에 데이터를 생성하는 것을 요청합니다. CRUD로 따지면 C입니다. 매 호출마다 새로운 데이터가 추가되기에, 비멱등성과 비안전성을 갖는다.

	PUT: 서버에 존재하는 데이터를 수정하거나 존재하지 않으면 생성합니다. CRUD로 따지면 C,U입니다. 리소스를 수정하기에 비안전성을 갖고, PUT 메서드의 요청을 여러 번 하더라도 한번 요청했을 때와 결과가 같기에 멱등성을 갖는다.
	
	PATCH: 서버에 존재하는 데이터를 일부 수정합니다. CRUD로 따지면 U입니다.

	DELETE: 서버에 데이터를 제거할 것을 요청합니다. 존재하지 않아도 동일하게 동작합니다. CRUD로 따지면 D입니다.

	HEAD: 서버 리소스의 헤더(메타 데이터의 취득)

	OPTIONS: 리소스가 지원하고 있는 메소드의 취득

	CONNECT: 프록시 동작의 터널 접속을 변경

  

- 안전성 (Safe) : GET, HEAD, OPTIONS

  

	HTTP는 안전한 메서드라 불리는 메서드의 집합이다.

	  

	안전한 메서드의 목적은 서버에 어떤 영향을 줄 수 있는 안전하지 않은 메서드가 사용될 때 사용자들에게 그 사실을 알려줄 수 있도록 하는 것이다.

	  

	읽기 전용인 경우 안전한 메서드로 간주하며, GET, HEAD, OPTIONS 메서드는 안전한 메서드로 정의되어 있다.

  

	즉, 리소스를 수정하지 않는 메소드들을 Safe 하다고 말한다.

- 멱등성(Idempotence) : PUT, DELETE, GET, HEAD, OPTIONS, TRACE

	멱등성이란 특정 메서드의 요청을 여러 번 하더라도 한번 요청했을 때와 결과가 같다.

	모든 안전한 메서드는 멱등성 또한 갖지만, 모든 멱등성을 지닌 메서드가 안전한 것은 아닙니다.

	PUT과 DELETE는 둘 다 멱등성을 가졌지만 안전하지는 않은 메서드입니다.

  

![](https://media.vlpt.us/images/nameunzz/post/d6dbb23c-826e-4006-993c-37c4805fbbdf/image.png)

- HTTP 응답 상태 코드

- 1 xx : (정보) 요청을 받았으며 프로세스를 계속한다

- 2 xx : (성공) 요청을 성공적으로 받았으며 인식해서 처리했다

- 3 xx : (리다이렉션) 요청 완료를 위해 추가 작업 조치가 필요하다.

- 4 xx : (클라이언트 에러)요청의 문법이 잘못되었거나 요청을 처리할 수 없다.

- 5 xx : (서버 에러) 서버가 명백히 유효한 요청에 대해 충족을 실패했다.

  

<br />

  

<div  id="2"></div>

  

## GET 방식

  

- 서버로부터 **정보 조회**하기 위하여 설계된 메소드입니다.

- Select의 성향을 가지고 있다. 서버에서 어떤 데이터를 가지고 와서 보여주는 용도이지 서버의 값이나 상태를 바꾸지는 않는다. 따라서 **동일한 요청을 여러 번 수행하더라도 동일한 응답이 와야한다**. (멱등성)

- GET은 HTTP Reqeust Message의 Header 부분의 파라미터에 요청 정보를 담아서 전송하는데, URL의 끝의 ? 뒤에 요청 정보가 (key=value)형태의 쌍을 이루어 이어서 붙는 식이다.

- URL에 요청 정보가 이어붙어 노출되기에 보안성에 취약하고 길이 제한이 있어 대용량 데이터 전송이 불가하다.

- ex

```

GET /user

```

데이터를 조회하는 것이기 때문에 요청시에 Body 값과 Content-Type 가 비워져있다.

조회할 데이터에 대한 정보는 URL을 통해서 파라메터를 받는다.

데이터 조회에 성공한다면(상태코드 : 200) Body 값에 데이터 값을 저장하여 성공 응답을 보낸다.

에러가 발생한다면 주로 404 (Not found) 에러나 400 (Bad request) 에러가 발생한다.

GET은 캐싱이 가능하여 같은 데이터를 한번 더 조회할 경우에 저장한 값을 사용하여 조회 속도가 빨라진다.

  

<br />

  

<div  id="3"></div>

  

## POST 방식

  

-  **정보 생성**하기 위해 설계된 메소드입니다.

- 서버의 값이나 상태를 바꾸기 위해서 사용한다.

- HTTP Request Message의 Body 부분에 요청 정보를 숨겨서 전송한다.

- HTTP 메세지의 Body는 길이의 제한 없이 데이터를 전송할 수 있어서 대용량의 데이터를 전송할 수 있다.

-  **서버에게 동일한 요청을 여러 번 전송해도 응답은 항상 다를 수 있다**. (멱등하지 않다.)

- ex

```

POST /user

body : {date : "example"}

Content-Type : "application/json"

```

데이터를 생성하는 것이기 때문에 요청시에 Body 값과 Content-Type 값을 작성해야한다.

URL을 통해서 데이터를 받지 않고, Body 값을 통해서 받는다.

데이터 조회에 성공한다면 Body 값에 저장한 데이터 값을 저장하여 성공 응답(상태 코드 : 201)을 보낸다.

  

<br />

  

<div  id="4"></div>

  

## PUT 방식

  

-  **정보 생성 / 업데이트**하기 위해 서버로 데이터를 보내는 데 사용됩니다.

- idempotent

- ex

```

PUT /user/1

body : {date : "update example"}

Content-Type : "application/json"

```

데이터를 수정하는 것이기 때문에 요청시에 Body 값과 Content-Type 값을 작성해야한다.

URL을 통해서 어떠한 데이터를 수정할지 파라메터를 받는다.

그리고 수정할 데이터 값을 Body 값을 통해서 받는다.

  

<br />

  

<div  id="5"></div>

  

## DELETE 방식

  

-  **정보 삭제**하기 위한 메소드.

- idempotent

- ex

```

DELETE /user/1

```

데이터를 삭제하는 것이기 때문에 요청시에 Body 값과 Content-Type 값이 비워져있다.

URL을 통해서 어떠한 데이터를 삭제할지 파라메터를 받는다.

데이터 삭제에 성공한다면 Body 값 없이 성공 응답만 보내게 된다.

  

<br />

  

<div  id="6"></div>

  

## 비교

  

### GET vs POST

  

GET은 SELECT 적인 성향을 갖고 있다. 반면에 POST 는 서버의 값이나 상태를 변경하기 위해서 또는 추가하기 위해서 사용된다.

  

부수적인 차이점을 좀 더 살펴보자면 GET 방식의 요청은 브라우저에서 Caching 할 수 있다. 때문에 POST 방식으로 요청해야 할 것을 보내는 데이터의 크기가 작고 보안적인 문제가 없다는 이유로 GET 방식으로 요청한다면 기존에 caching 되었던 데이터가 응답될 가능성이 존재한다. 때문에 목적에 맞는 기술을 사용해야 한다.

 

### 🔑POST vs PUT

> 자원에 대한 행위를 나타내는 4가지 Method는 CRUD(Create/Read/Update/Delete)에 각각 매칭된다.

POST는 Create(생성), PUT은 Update(수정)에 매칭되는데, RESTful API는 자원에 대한 행위를 4가지 Method로 표한하니까,  _자원에 대한 생성은 POST_가 담당하고,  _자원에 대한 수정은 PUT_이 담당하는 것이다.

POST는 새로운 데이터를 계속 생성하기 때문에 요청시마다 데이터를 생성하지만, PUT은 사용자가 데이터를 지정하고 수정하는 것이기 때문에 같은 요청을 계속하더라도 데이터가 계속 생성되지는 않는다.

보통 이렇게 정의하지만, 나도 이런 정의만 보고 도대체 어떻게 다른지 감을 잡기 힘들었다. 여러분들은 이런 어려움이 없으면 하는 마음에 자세하게 예를 들어 설명해보겠다.

아래와 같은 URI가 있고, 해당 URI에 대해 POST와 PUT이 작동하는 예를 보자.  
`/student`

POST 메소드로 뽀로로라는 이름을 가진 학생을 생성하기 위에 아래와 같이 요청하면, 고유 구분값인 id를 1로 설정되어 뽀로로라는 학생이 생성된다.

```null
HttpRequest
POST /student
{
  “name”: “뽀로로”,
  “grade”: 1
}

HttpResponse
HTTP/1.1 200 OK
{
  “id”: 1,
  “name”: “뽀로로”,
  “grade”: 1
}
```

그러면 이제, PUT을 통해 뽀로로의 grade를 2를 변경해보자. PUT은 리소스에 대한 수정이므로 특정 리소스를 구분하는 id값을 넣어줘야 한다.

```null
HttpRequest
PUT /student/1
{
  “grade”: 2
}

HttpResponse
HTTP/1.1 200 OK
{
  “id”: 1,
  “name”: “뽀로로”,
  “grade”: 2
}
```

이는 POST와 PUT의 가장 기본적인 사용예제이고, 두 메서드의 차이를 조금 더 자세히 알아보기 위한 예제를 또 살펴보자.

POST 메서드로 뽀로로 학생을 생성해달라고 2번 요청하면 어떻게 될까?

```null
POST /student
{
   “name”: “뽀로로”,
   “grade”: 1
}
```

id가 1과 2인 뽀로로가 두 개가 생겨버린다. POST는 리소스를 생성하기 위한 메서드로 요청한 횟수마다 새로운 리소스를 생성한다.  
(물론 name을 unique key로 잡으면 같은 이름으로 생성하지 안되게 만들 수는 있다.)

```null
HTTP/1.1 200 OK
{ “id”: 1, “name”: “뽀로로”, “grade”: 1 }

HTTP/1.1 200 OK
{ “id”: 2, “name”: “뽀로로”, “grade”: 1}
```

반대로 PUT으로 같은 요청을 두번 보내면 어떻게 될까?

```null
PUT /student/3
{
  “name”: ”에디”
  “grade”: 2
}
```

2번 아니, 수백번 보내도 아래와 같이 같은 응답이 온다. id를 3을 가진 리소스는 없었으므로, 최소 한번은 생성되고, 그 후에는 생성되지 않는다.

```null
HTTP/1.1 200 OK
{ “id”: ”3”, “name”: “에디”, “grade”: 2 }
```

예시를 들며 설명했던 내용을 다시 정리해보면,

-   POST  
    _POST는 리소스의 생성을 담당한다.  
    _POST는 요청 시 마다, 새로운 리소스가 생성된다.
-   PUT  
    _PUT은 리소스의 생성과 수정을 담당한다.  
    _PUT은 요청 시 마다, 같은 리소스를 반환한다  
    * 물론, 리소스 안에 속성은 변경될 수 있다.

이를 어려운 말로 이야기하면,  _PUT은 멱등하다_고 말할 수 있고,  _POST는 멱등하지 않다_라고 말한다.

  

### PUT vs PATCH

  

둘 다 데이터의 수정을 위한 method이다.

  

자원의 일부를 수정할 때는 PATCH를, 전체적인 수정이 필요할 때는 PUT을 이용하는 것이 적절하다.

  

- ex

**PUT** 요청 시 요청을 일부분만 보낸 경우 나머지는 default 값으로 수정되는 게 원칙이므로,

바뀌지 않는 속성도 모두 보내야 한다.

(만약 전체가 아닌 일부만 전달할 경우, 전달한 필드외 모두 null 혹은 default 값처리되니 주의해야한다.)

예를 들어, PUT HTTP 메소드로 gildong 이라는 유저의 나이(age)를 15로 변경하고자 할때

수정된 값만 보낼 경우, 보내지 않은 데이터는 null로 변경되어 버린다.

```

PUT /users/1

{

"age": 15

}

HTTP/1.1 200 OK

{

"name": null,

"age": 15

}

```

따라서, PUT 요청 시에는 아래와 같이 변경되지 않는 데이터도 모두 전달해야한다.

```

PUT /users/1

{

"name": "gildong",

"age": 15

}

HTTP/1.1 200 OK

{

"name": "gildong",

"age": 15

}

```

그러나 PATCH를 이용하여 ‘age’만 변경하는 요청을 보내면,

새롭게 바뀐 부분만 반영되며 나머지는 기존의 데이터가 유지된다.

```

PATCH /users/1

{

"age": 15

}

HTTP/1.1 200 OK

{

"name": "gildong",

"age": 15

}

```