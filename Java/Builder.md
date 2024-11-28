# Builder

- [Builder](#builder)
    - [1. 빌더 패턴 (Builder Pattern)](#1-빌더-패턴-builder-pattern)
      - [예제 코드 (리마인더)](#예제-코드-리마인더)
    - [2. 빌더 어노테이션 (Builder Annotation)](#2-빌더-어노테이션-builder-annotation)
      - [Lombok의 `@Builder` 어노테이션](#lombok의-builder-어노테이션)
      - [예제 코드 (`@Builder` 사용)](#예제-코드-builder-사용)
      - [주요 기능](#주요-기능)
    - [빌더 패턴과 빌더 어노테이션 비교](#빌더-패턴과-빌더-어노테이션-비교)
    - [장점과 고려사항](#장점과-고려사항)
      - [장점](#장점)
      - [고려사항](#고려사항)
    - [요약](#요약)

### 1. 빌더 패턴 (Builder Pattern)

빌더 패턴은 이전에 설명한 것처럼, 복잡한 객체의 생성 과정을 간소화하기 위해 사용되는 디자인 패턴입니다. 빌더 패턴은 객체의 여러 필드를 단계적으로 설정하고 최종적으로 객체를 생성하는 방식으로, 복잡한 생성자나 많은 매개변수를 요구하는 경우에 특히 유용합니다.

주요 장점으로는 가독성을 높이고, 객체의 일관된 상태를 보장하며, 객체를 점진적으로 설정할 수 있다는 점이 있습니다.

#### 예제 코드 (리마인더)

```java
public class Car {
    private String engine;
    private int wheels;
    private String color;

    public static class Builder {
        private String engine;
        private int wheels;
        private String color;

        public Builder engine(String engine) {
            this.engine = engine;
            return this;
        }

        public Builder wheels(int wheels) {
            this.wheels = wheels;
            return this;
        }

        public Builder color(String color) {
            this.color = color;
            return this;
        }

        public Car build() {
            return new Car(this);
        }
    }

    private Car(Builder builder) {
        this.engine = builder.engine;
        this.wheels = builder.wheels;
        this.color = builder.color;
    }
}
```

위의 코드는 수동으로 작성된 빌더 패턴입니다. `Builder` 내부 클래스는 `Car` 객체의 각 필드를 설정하는 메서드를 제공하며, 메서드 체이닝 방식으로 각 속성을 설정하고 마지막으로 `build()` 메서드를 호출해 객체를 생성합니다.

### 2. 빌더 어노테이션 (Builder Annotation)

빌더 어노테이션은 빌더 패턴을 더 간단하고 쉽게 사용하도록 지원하는 도구입니다. 일반적으로 많이 사용되는 빌더 어노테이션은 **Lombok** 라이브러리의 `@Builder`입니다. 이 어노테이션을 사용하면 빌더 패턴을 구현할 때 수동으로 빌더 클래스를 작성하지 않아도 됩니다.

#### Lombok의 `@Builder` 어노테이션

- **Lombok**은 자바 개발의 생산성을 높여주는 라이브러리로, 반복적인 코드를 줄여줍니다.
- `@Builder` 어노테이션을 사용하면 빌더 패턴을 사용한 객체 생성을 간편하게 작성할 수 있습니다.

#### 예제 코드 (`@Builder` 사용)

```java
import lombok.Builder;
import lombok.ToString;

@Builder
@ToString
public class Car {
    private String engine;
    private int wheels;
    private String color;

    public static void main(String[] args) {
        Car car = Car.builder()
                .engine("V8")
                .wheels(4)
                .color("Red")
                .build();

        System.out.println(car);
    }
}
```

위의 예제에서 `@Builder` 어노테이션을 사용하면 Lombok이 자동으로 `Car` 클래스에 빌더 클래스를 생성합니다. 이 코드는 다음과 같은 장점을 가지고 있습니다.

- **간결함**: 수동으로 빌더 클래스를 작성할 필요 없이, Lombok이 자동으로 생성해 줍니다.
- **유지보수성**: 빌더 패턴을 수동으로 작성할 때 실수할 가능성이 줄어들고, 필드 추가/변경 시 수동으로 빌더를 수정할 필요가 없습니다.
- **가독성**: 코드가 짧아지기 때문에 가독성이 높아지고, 명시적인 `builder()` 호출로 빌더 패턴을 쉽게 이해할 수 있습니다.

#### 주요 기능

- `@Builder`는 `Car.builder()`를 호출하여 빌더 객체를 생성하고, 필드를 설정한 후 `build()` 메서드로 객체를 최종 생성합니다.
- `@ToString`은 `System.out.println(car)`와 같은 방식으로 객체의 내용을 출력할 때 가독성 있는 문자열로 출력되도록 지원합니다.

### 빌더 패턴과 빌더 어노테이션 비교

- **빌더 패턴**: 디자인 패턴의 일종으로, 복잡한 객체 생성을 쉽게 만들기 위한 구조입니다. 수동으로 빌더 클래스를 정의하고, 각 필드를 설정하며 최종 객체를 생성합니다.
- **빌더 어노테이션**: Lombok 같은 라이브러리를 사용해 빌더 패턴을 자동으로 구현하는 도구입니다. 개발자가 반복적인 빌더 작성 코드를 수동으로 구현할 필요 없이, 어노테이션을 통해 간결하게 빌더 패턴을 적용할 수 있습니다.

### 장점과 고려사항

#### 장점

- **자동 코드 생성**: Lombok의 `@Builder` 어노테이션을 통해 빌더 패턴을 빠르게 구현할 수 있습니다.
- **중복 제거**: 수동으로 작성해야 하는 빌더 코드를 줄임으로써 생산성을 높입니다.
- **유지보수 용이**: Lombok을 사용하면 클래스 필드가 변경될 때마다 빌더 클래스를 직접 수정할 필요가 없습니다.

#### 고려사항

- **외부 라이브러리 의존성**: Lombok은 외부 라이브러리이기 때문에 프로젝트에 이를 추가해야 합니다.
- **IDE 및 빌드 도구 호환성**: Lombok을 사용할 때 일부 IDE나 빌드 도구에서 호환성 문제가 발생할 수 있습니다. 이를 해결하려면 Lombok 플러그인을 설치하거나 추가 설정이 필요할 수 있습니다.

### 요약

- **빌더 패턴**은 복잡한 객체 생성을 간단하게 하기 위한 디자인 패턴으로, 주로 여러 필드가 있는 객체를 생성할 때 사용합니다.
- **빌더 어노테이션** (`@Builder`)은 Lombok 라이브러리를 통해 빌더 패턴을 자동으로 적용하는 방법으로, 개발자가 반복적인 빌더 클래스를 작성할 필요 없이 객체 생성을 간단하게 할 수 있도록 지원합니다.