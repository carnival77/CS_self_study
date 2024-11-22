# JSON 직렬화 및 역직렬화 

---
- [JSON 직렬화 및 역직렬화](#json-직렬화-및-역직렬화)
    - [1. JSON 직렬화 (Serialization)](#1-json-직렬화-serialization)
      - [주요 목적](#주요-목적)
      - [예제 코드 (Jackson 사용)](#예제-코드-jackson-사용)
      - [결과](#결과)
    - [2. JSON 역직렬화 (Deserialization)](#2-json-역직렬화-deserialization)
      - [주요 목적](#주요-목적-1)
      - [예제 코드 (Jackson 사용)](#예제-코드-jackson-사용-1)
      - [결과](#결과-1)
    - [3. 직렬화와 역직렬화에 사용되는 Jackson의 주요 어노테이션들](#3-직렬화와-역직렬화에-사용되는-jackson의-주요-어노테이션들)
      - [주요 어노테이션들](#주요-어노테이션들)
      - [예제 코드 (어노테이션 사용)](#예제-코드-어노테이션-사용)
    - [요약](#요약)
    - [1. `@JsonNaming(PropertyNamingStrategies.SnakeCaseStrategy.class)`](#1-jsonnamingpropertynamingstrategiessnakecasestrategyclass)
      - [예제 코드](#예제-코드)
    - [2. `@JsonProperty`](#2-jsonproperty)
      - [주요 기능](#주요-기능)
      - [예제 코드](#예제-코드-1)
    - [3. `@JsonIgnore`](#3-jsonignore)
      - [주요 기능](#주요-기능-1)
      - [예제 코드](#예제-코드-2)
    - [요약](#요약-1)
---

**JSON 직렬화 (Serialization)**와 **역직렬화 (Deserialization)**는 객체 지향 프로그래밍에서 객체와 JSON 데이터 간의 변환을 의미합니다. 특히 웹 애플리케이션에서 데이터 교환을 위해 자주 사용되며, **Jackson**, **Gson**과 같은 라이브러리들이 Java에서 이러한 작업을 수행하는 데 사용됩니다. 각각의 개념과 그 과정을 구체적으로 살펴보겠습니다.

### 1. JSON 직렬화 (Serialization)

JSON 직렬화는 **Java 객체를 JSON 형식의 문자열로 변환하는 과정**을 의미합니다. 이를 통해 객체를 파일에 저장하거나 네트워크를 통해 다른 시스템에 전송할 수 있습니다.

#### 주요 목적

- **데이터 전송**: 서버와 클라이언트 사이에 객체 데이터를 전송할 수 있도록 JSON 형식으로 변환합니다.
- **파일 저장**: 객체의 데이터를 파일 형태로 저장하여, 나중에 데이터를 다시 불러올 수 있습니다.

#### 예제 코드 (Jackson 사용)

아래는 Jackson 라이브러리를 사용하여 Java 객체를 JSON으로 직렬화하는 예제입니다.

```java
import com.fasterxml.jackson.databind.ObjectMapper;

public class Main {
    public static void main(String[] args) {
        try {
            // 객체 생성
            User user = new User();
            user.setUsername("johndoe");
            user.setAge(30);

            // ObjectMapper 인스턴스 생성
            ObjectMapper objectMapper = new ObjectMapper();

            // 객체를 JSON 문자열로 직렬화
            String jsonString = objectMapper.writeValueAsString(user);
            System.out.println(jsonString);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

class User {
    private String username;
    private int age;

    // Getter & Setter
    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

#### 결과

```json
{"username":"johndoe","age":30}
```

이 코드에서는 `ObjectMapper`를 사용하여 `User` 객체를 JSON 문자열로 변환합니다.

### 2. JSON 역직렬화 (Deserialization)

역직렬화는 **JSON 문자열을 Java 객체로 변환하는 과정**을 의미합니다. 서버에서 받은 JSON 데이터나 파일에 저장된 JSON 데이터를 Java 프로그램에서 사용하려면 이를 객체로 변환해야 합니다.

#### 주요 목적

- **데이터 파싱**: JSON 데이터를 객체로 변환하여 프로그램에서 쉽게 사용할 수 있도록 합니다.
- **시스템 간 데이터 전송**: JSON으로 전송된 데이터를 원래의 객체로 변환하여 시스템 간의 데이터 호환성을 유지합니다.

#### 예제 코드 (Jackson 사용)

아래는 JSON 문자열을 Java 객체로 역직렬화하는 예제입니다.

```java
import com.fasterxml.jackson.databind.ObjectMapper;

public class Main {
    public static void main(String[] args) {
        try {
            // JSON 문자열
            String jsonString = "{\"username\":\"johndoe\",\"age\":30}";

            // ObjectMapper 인스턴스 생성
            ObjectMapper objectMapper = new ObjectMapper();

            // JSON 문자열을 객체로 역직렬화
            User user = objectMapper.readValue(jsonString, User.class);
            System.out.println("Username: " + user.getUsername());
            System.out.println("Age: " + user.getAge());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

class User {
    private String username;
    private int age;

    // Getter & Setter
    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

#### 결과

```json
Username: johndoe
Age: 30
```

이 예제에서 `ObjectMapper`의 `readValue()` 메서드를 사용하여 JSON 문자열을 `User` 객체로 변환하고, 그 결과를 출력합니다.

### 3. 직렬화와 역직렬화에 사용되는 Jackson의 주요 어노테이션들

JSON 직렬화 및 역직렬화를 효과적으로 관리하기 위해 Jackson은 다양한 어노테이션을 제공합니다. 이들은 JSON과 Java 객체 간 변환 규칙을 정의할 때 유용합니다.

#### 주요 어노테이션들

- **`@JsonProperty`**: 특정 필드를 JSON에서의 특정 이름과 매핑합니다. 이름이 일치하지 않거나 명확하게 정의해야 할 경우 사용됩니다.
- **`@JsonIgnore`**: 특정 필드를 JSON 변환 시 무시하도록 설정합니다. 민감한 데이터나 불필요한 데이터를 JSON에서 제외할 때 유용합니다.
- **`@JsonNaming`**: JSON 필드의 명명 규칙을 설정합니다 (`SnakeCase`, `CamelCase` 등). 클래스 전체에 적용하여 JSON과 Java 객체의 필드 명명 방식이 일관되도록 만듭니다.
- **`@JsonInclude`**: null인 필드나 기본값을 가지는 필드를 JSON 변환에서 제외하는 규칙을 정의합니다.

#### 예제 코드 (어노테이션 사용)

```java
import com.fasterxml.jackson.annotation.JsonIgnore;
import com.fasterxml.jackson.annotation.JsonProperty;

public class User {
    @JsonProperty("user_name")
    private String username;

    private int age;

    @JsonIgnore
    private String password;

    // Getter & Setter
    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }
}
```

위 예제에서 `@JsonProperty("user_name")`은 필드를 `user_name`이라는 JSON 필드명으로 매핑하고, `@JsonIgnore`는 `password` 필드를 JSON에서 제외시킵니다.

### 요약

- **JSON 직렬화**: Java 객체를 JSON 문자열로 변환합니다. 데이터를 네트워크로 전송하거나 파일에 저장하기 위해 사용됩니다.
- **JSON 역직렬화**: JSON 문자열을 Java 객체로 변환합니다. JSON 데이터를 프로그램에서 쉽게 사용할 수 있도록 합니다.
- **Jackson**: Jackson 라이브러리는 이러한 JSON 직렬화 및 역직렬화 과정을 간단하고 직관적으로 구현할 수 있도록 돕습니다. 주요 어노테이션들은 변환 규칙을 정의하여 JSON과 Java 객체 간의 호환성을 높입니다.



### 1. `@JsonNaming(PropertyNamingStrategies.SnakeCaseStrategy.class)`

`@JsonNaming`은 클래스 또는 필드의 이름을 JSON 형식에 맞춰 자동으로 변환하도록 지정하는 Jackson 어노테이션입니다. 이 어노테이션은 객체의 필드 이름을 특정한 네이밍 규칙에 따라 변환할 수 있게 해줍니다.

- **`PropertyNamingStrategies.SnakeCaseStrategy`**: 이 전략은 JSON 필드 이름을 **스네이크 케이스**로 변환합니다. 스네이크 케이스란 단어 사이에 언더스코어(`_`)를 사용하는 명명 규칙입니다.

예를 들어, 클래스의 필드 이름이 `firstName`이라면, 이 어노테이션을 사용하여 JSON 형식으로 변환하면 `first_name`으로 변환됩니다.

#### 예제 코드

```java
import com.fasterxml.jackson.databind.PropertyNamingStrategies;
import com.fasterxml.jackson.databind.annotation.JsonNaming;

@JsonNaming(PropertyNamingStrategies.SnakeCaseStrategy.class)
public class User {
    private String firstName;
    private String lastName;

    // Getter & Setter
}
```

위 클래스가 JSON으로 직렬화되면 다음과 같은 형태가 됩니다:

```json
{
  "first_name": "John",
  "last_name": "Doe"
}
```

### 2. `@JsonProperty`

`@JsonProperty`는 JSON 데이터의 필드와 Java 객체의 필드 간의 이름을 매핑하는 역할을 합니다. 이 어노테이션은 JSON 직렬화/역직렬화 시에 필드의 이름을 명시적으로 지정하고자 할 때 사용됩니다.

#### 주요 기능

- **필드 이름 변경**: JSON과 Java 클래스의 필드 이름이 다를 때 이를 맞춰주기 위해 사용됩니다.
- **명시적 매핑**: 필드가 직렬화/역직렬화 시에 특정 이름으로 사용되도록 지정합니다.

#### 예제 코드

```java
import com.fasterxml.jackson.annotation.JsonProperty;

public class User {
    @JsonProperty("user_name")
    private String username;

    private int age;

    // Getter & Setter
}
```

위의 경우, `username` 필드는 JSON으로 직렬화될 때 `user_name`이라는 이름으로 나타납니다. 즉, JSON 출력은 다음과 같습니다:

```json
{
  "user_name": "johndoe",
  "age": 30
}
```

이런 방식으로 객체 필드와 JSON 필드 사이에 맞지 않는 이름을 매핑하여 호환성을 보장할 수 있습니다.

### 3. `@JsonIgnore`

`@JsonIgnore`는 JSON 직렬화 또는 역직렬화 과정에서 해당 필드를 무시하도록 지정하는 어노테이션입니다. 이 어노테이션은 특정 필드를 JSON으로 내보내거나 JSON에서 읽어들일 때 무시하고자 할 때 사용합니다.

#### 주요 기능

- **필드 무시**: 민감한 정보, 필요 없는 데이터, 또는 내부 사용을 위한 데이터를 JSON으로 직렬화하지 않도록 방지합니다.
- **커스터마이즈**: 특정한 로직에 의해 JSON에 포함되지 않아야 할 필드를 명시적으로 지정합니다.

#### 예제 코드

```java
import com.fasterxml.jackson.annotation.JsonIgnore;

public class User {
    private String username;

    @JsonIgnore
    private String password;

    // Getter & Setter
}
```

위의 예제에서 `password` 필드는 JSON으로 직렬화되지 않습니다. 예를 들어, 다음과 같은 결과를 얻게 됩니다:

```json
{
  "username": "johndoe"
}
```

`password` 필드는 JSON에 포함되지 않기 때문에 보안이 필요한 경우 또는 필요 없는 데이터를 배제하는 데 유용합니다.

### 요약

- **`@JsonNaming(PropertyNamingStrategies.SnakeCaseStrategy.class)`**: JSON 직렬화/역직렬화 시 클래스의 필드 이름을 스네이크 케이스로 자동 변환합니다.
- **`@JsonProperty`**: 필드 이름을 JSON에서 명시적으로 지정하여 필드 매핑을 커스터마이즈합니다.
- **`@JsonIgnore`**: JSON 직렬화/역직렬화 과정에서 특정 필드를 무시합니다.

이 어노테이션들을 사용하면 Jackson을 이용한 JSON 변환 과정에서 유연하게 필드 이름을 제어하고, 특정 필드의 노출 여부를 관리할 수 있어 개발자의 의도에 맞게 JSON 구조를 다룰 수 있습니다.