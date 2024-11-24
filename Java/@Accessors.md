# @Accessors

---

- [@Accessors](#accessors)
    - [`@Accessors(chain = true)`의 의미](#accessorschain--true의-의미)
      - [예제 코드 (`@Accessors(chain = true)` 사용)](#예제-코드-accessorschain--true-사용)
    - [어떻게 동작하는가?](#어떻게-동작하는가)
      - [예시 비교](#예시-비교)
        - [1. **일반적인 Setter 사용** (메서드 체이닝 없음)](#1-일반적인-setter-사용-메서드-체이닝-없음)
        - [2. **`@Accessors(chain = true)` 사용** (메서드 체이닝 사용)](#2-accessorschain--true-사용-메서드-체이닝-사용)
    - [옵션: `@Accessors(fluent = true)`와 비교](#옵션-accessorsfluent--true와-비교)
      - [예시 (`fluent = true`)](#예시-fluent--true)
    - [요약](#요약)
---

`@Accessors(chain = true)`는 **Lombok** 라이브러리에서 제공하는 어노테이션으로, 필드에 대해 생성된 getter와 setter 메서드의 동작 방식을 변경하는 데 사용됩니다. 이 어노테이션은 메서드 체이닝을 가능하게 해줍니다.

아래에서 `@Accessors(chain = true)`의 의미를 상세히 설명하겠습니다.

### `@Accessors(chain = true)`의 의미

- **Lombok**의 `@Accessors` 어노테이션은 getter/setter 메서드의 접근 방식을 제어합니다.
- `chain = true` 설정을 추가하면 **메서드 체이닝**이 가능해지도록 각 setter 메서드가 객체 자신의 인스턴스를 반환하게 됩니다.

간단히 말해, 필드 값을 설정할 때마다 setter 메서드가 객체 자신을 반환하여 여러 필드 값을 연속적으로 설정하는 **메서드 체이닝** 방식이 가능해집니다.

#### 예제 코드 (`@Accessors(chain = true)` 사용)

```java
import lombok.Getter;
import lombok.Setter;
import lombok.experimental.Accessors;

@Getter
@Setter
@Accessors(chain = true)
public class Person {
    private String name;
    private int age;

    public static void main(String[] args) {
        Person person = new Person()
                .setName("Alice")
                .setAge(25);

        System.out.println(person.getName()); // "Alice"
        System.out.println(person.getAge());  // 25
    }
}
```

### 어떻게 동작하는가?

- **기본적인 Setter 동작**: 일반적인 setter 메서드는 void를 반환합니다. 예를 들어 `person.setName("Alice")`는 이름을 설정하고 끝나기 때문에 다른 필드 값을 설정하려면 다음 줄에 또다시 객체를 사용해야 합니다.
- **메서드 체이닝**: `@Accessors(chain = true)`를 사용하면 각 setter 메서드가 `this`를 반환합니다. 이로 인해 여러 필드를 한 번에 설정할 수 있으며, 코드의 가독성이 좋아지고 사용이 간편해집니다.

#### 예시 비교

##### 1. **일반적인 Setter 사용** (메서드 체이닝 없음)

```java
Person person = new Person();
person.setName("Alice");
person.setAge(25);
```

위와 같은 일반적인 방식은 각 필드 설정을 별도의 줄에서 해야 하므로 코드가 조금 더 길어지고 가독성이 떨어질 수 있습니다.

##### 2. **`@Accessors(chain = true)` 사용** (메서드 체이닝 사용)

```java
Person person = new Person()
        .setName("Alice")
        .setAge(25);
```

위 방식에서는 메서드 체이닝을 사용하여 연속적으로 여러 필드의 값을 설정할 수 있습니다. 코드가 더 간결하고 직관적입니다.

### 옵션: `@Accessors(fluent = true)`와 비교

- **`@Accessors(fluent = true)`**: 이 옵션을 사용하면 getter와 setter 메서드의 이름에서 `get`/`set` 접두어를 없애고 필드 이름 자체로 메서드를 호출합니다.

  예를 들어 `name` 필드에 대해 `setName(String name)` 대신 `name(String name)`으로 호출할 수 있습니다.

#### 예시 (`fluent = true`)

```java
@Accessors(fluent = true)
public class Person {
    private String name;
    private int age;

    // 사용 예시
    public static void main(String[] args) {
        Person person = new Person()
                .name("Alice")   // setName() 대신 name() 사용
                .age(25);        // setAge() 대신 age() 사용

        System.out.println(person.name()); // getName() 대신 name() 사용
    }
}
```

### 요약

- `@Accessors(chain = true)`는 Lombok의 어노테이션으로 **setter 메서드가 객체 자신을 반환하게** 하여 메서드 체이닝을 가능하게 해줍니다.
- 이를 통해 여러 필드 값을 설정할 때 **코드를 간결하고 가독성 있게 작성**할 수 있습니다.
- `@Accessors` 어노테이션은 다양한 옵션을 제공하며, 상황에 맞게 체이닝 또는 fluent 스타일을 사용할 수 있습니다.