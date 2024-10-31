# CORS

---

- [CORS](#cors)
  - [CORS란 무엇인가?](#cors란-무엇인가)
  - [오리진(Origin)이란?](#오리진origin이란)
  - [구체적인 예시로 보는 CORS 문제와 해결](#구체적인-예시로-보는-cors-문제와-해결)
    - [상황 설명](#상황-설명)
    - [해결 방법 (CORS 설정)](#해결-방법-cors-설정)
    - [**구체적 예시 코드**](#구체적-예시-코드)
      - [개별 Controller에 CORS 설정하기](#개별-controller에-cors-설정하기)
      - [전역적으로 CORS 설정하기](#전역적으로-cors-설정하기)
    - [요약](#요약)

---

## CORS란 무엇인가?

**CORS (Cross-Origin Resource Sharing)**는 **다른 오리진(출처)에서 자원을 요청할 때 발생하는 보안 문제를 해결하는 메커니즘**입니다. 웹 브라우저는 보안을 위해 기본적으로 다른 오리진에서의 요청을 차단하는 **동일 출처 정책(Same-Origin Policy)**을 가지고 있습니다. 이를 우회하여 리소스를 공유할 수 있도록 허용하는 것이 바로 CORS입니다.

## 오리진(Origin)이란?

오리진은 **프로토콜 + 도메인(호스트 이름) + 포트 번호**의 조합을 의미합니다. 예를 들어, 다음과 같은 URL을 보면:

- `http://example.com:3000`
- `https://api.example.com`

이 두 URL은 **프로토콜**, **도메인**, **포트** 중 하나라도 다르기 때문에 서로 다른 오리진입니다. 브라우저는 보안 상 이유로 오리진이 다른 웹사이트에서 자원을 가져오려 할 때 이를 차단하게 되는데, 이로 인해 발생하는 문제가 **CORS**입니다.

------

## 구체적인 예시로 보는 CORS 문제와 해결

### 상황 설명

당신은 두 가지 웹 애플리케이션을 운영하고 있다고 가정해봅시다:

1. **프론트엔드 웹사이트**: `http://frontend.com` (사용자가 접속하여 보게 되는 사이트)
2. **백엔드 API 서버**: `http://api.backend.com` (프론트엔드에서 데이터를 가져오기 위해 사용하는 서버)

**문제 발생**:

- 사용자가 `http://frontend.com`에 접속하여 **API 데이터를 가져오려** 합니다. 이때 `http://frontend.com`에서 `http://api.backend.com`의 데이터를 요청합니다.
- 하지만 브라우저는 이 두 도메인이 서로 다르다고 인식하고, **보안을 위해 기본적으로 데이터를 차단**합니다. 이로 인해 **CORS 에러**가 발생하게 됩니다.
- 이러한 상황이 발생하는 이유는 두 오리진(`http://frontend.com`과 `http://api.backend.com`)이 서로 다르기 때문입니다. 브라우저는 "다른 출처의 자원을 가져오는 것을 제한"하는 **동일 출처 정책**을 강제하기 때문에, 데이터를 가져올 수 없습니다.

### 해결 방법 (CORS 설정)

이 문제를 해결하기 위해 **백엔드 서버에서 CORS 설정을 추가**해야 합니다. 즉, 백엔드 서버가 특정 오리진에서의 요청을 허용하도록 설정하는 것입니다.

1. **서버 측 CORS 설정**
   백엔드 서버인 `http://api.backend.com`에 다음과 같은 설정을 추가합니다:

   ```
   http
   
   Access-Control-Allow-Origin: http://frontend.com
   ```

   이 설정은 백엔드 서버가 **특정 오리진(`http://frontend.com`)에서 오는 요청**을 허용하도록 만들어줍니다. 이제 백엔드 서버는 `http://frontend.com`에서 오는 데이터 요청을 허락하게 됩니다.

2. **브라우저의 동작**
   사용자가 `http://frontend.com`에 접속하여 데이터를 요청하면, 요청이 `http://api.backend.com`으로 전송됩니다.
   백엔드 서버는 응답에 **`Access-Control-Allow-Origin: http://frontend.com`** 헤더를 포함시켜 브라우저에 전송하고, 브라우저는 이 헤더를 보고 해당 요청이 허용된 것임을 확인합니다.
   결과적으로, 브라우저는 데이터를 정상적으로 사용할 수 있게 됩니다.

### **구체적 예시 코드** 

#### 개별 Controller에 CORS 설정하기

개별 컨트롤러에서 특정 오리진을 허용하는 방법입니다. `@CrossOrigin` 어노테이션을 사용하여 특정 도메인에서의 요청을 허용할 수 있습니다.

```java
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@CrossOrigin(origins = "http://frontend.com") // 특정 오리진 허용
public class ApiController {

    @GetMapping("/data")
    public String getData() {
        return "Hello from backend!";
    }
}
```

위의 코드에서는 `@CrossOrigin` 어노테이션을 사용하여 **`http://frontend.com`**에서 오는 요청을 허용하도록 설정했습니다. 이렇게 설정하면 이 컨트롤러에 속한 모든 요청이 특정 오리진에서의 요청에 대해 허용됩니다.

#### 전역적으로 CORS 설정하기

모든 컨트롤러와 엔드포인트에 대해 전역적으로 CORS 설정을 하려면 `WebMvcConfigurer`를 구현하여 설정할 수 있습니다.

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.CorsRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

@Configuration
public class WebConfig {

    @Bean
    public WebMvcConfigurer corsConfigurer() {
        return new WebMvcConfigurer() {
            @Override
            public void addCorsMappings(CorsRegistry registry) {
                registry.addMapping("/**")  // 모든 경로에 대해 적용
                        .allowedOrigins("http://frontend.com") // 허용할 오리진 설정
                        .allowedMethods("GET", "POST", "PUT", "DELETE") // 허용할 HTTP 메서드
                        .allowedHeaders("*"); // 허용할 헤더 설정
            }
        };
    }
}
```

위 코드에서:

- `@Configuration`을 사용하여 **전역 CORS 설정을 정의**합니다.
- `addCorsMappings()` 메서드를 통해 모든 엔드포인트(`/**`)에 대해 **`http://frontend.com`**에서 오는 요청을 허용하도록 설정했습니다.
- 추가로 `allowedMethods()`를 사용하여 **허용할 HTTP 메서드**를 지정하고, `allowedHeaders()`를 통해 **허용할 요청 헤더**를 정의할 수 있습니다.

이렇게 하면 스프링 애플리케이션 전체에 대해 CORS 규칙이 적용되므로, 개별 컨트롤러마다 설정하지 않아도 됩니다.

위 코드는 **백엔드 서버(`http://api.backend.com`)에서 오는 모든 응답에 대해** `http://frontend.com`에서 오는 요청만 허용하도록 설정합니다.

------

### 요약

- **CORS란**: 다른 오리진에서 자원을 요청할 때 브라우저에서 발생하는 보안 문제를 해결하기 위한 메커니즘입니다.
- **문제**: 서로 다른 오리진에서 데이터를 요청하면 브라우저가 보안상의 이유로 이를 차단합니다.
- **해결 방법**: 백엔드 서버에서 `Access-Control-Allow-Origin` 헤더를 사용하여 특정 오리진에 대한 접근을 허용하면, 다른 도메인에서도 데이터를 사용할 수 있습니다.