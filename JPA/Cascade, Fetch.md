### 1. **Cascade 옵션의 필요성**

**`Cascade`** 옵션은 엔티티 간의 부모-자식 관계에서, 부모 엔티티의 작업(저장, 삭제 등)이 자식 엔티티에도 전파되도록 하는 설정입니다. 이를 통해 **참조 무결성**을 보장하고 개발자가 수동으로 관리해야 하는 작업을 자동화해 줍니다.

#### 1.1 **Cascade 옵션의 이유**

- **참조 무결성 유지**:

  - 부모 엔티티가 삭제되면 자식 엔티티도 함께 삭제되어야 하는 경우가 있습니다. 예를 들어, `Survey`가 삭제되면 관련된 모든 `SurveyVersion`도 삭제되어야 데이터가 일관성을 유지할 수 있습니다. 만약 `Survey`만 삭제되고 `SurveyVersion`이 남아 있다면 고아 데이터(부모가 없는 자식 데이터)가 발생합니다. 이는 데이터베이스의 참조 무결성에 위배됩니다.

  ```
  java코드 복사@ManyToOne(fetch = FetchType.LAZY, cascade = CascadeType.ALL)
  private Survey survey;
  ```

  - **`CascadeType.ALL`**을 설정하면 `Survey`가 삭제될 때 `SurveyVersion`, `SurveyItem` 등 모든 관련 자식들이 자동으로 삭제되므로 참조 무결성을 유지할 수 있습니다.

- **개발 편의성**:

  - 만약 Cascade 설정이 없다면, 부모 엔티티와 관련된 자식 엔티티들을 모두 직접 삭제하거나 저장해야 합니다. 이것은 개발자의 코드를 복잡하게 만들고, 실수로 데이터의 일관성을 깨트릴 가능성을 증가시킵니다. **Cascade 설정**을 통해 부모 엔티티와 자식 엔티티 간의 일관된 동작을 보장할 수 있습니다.

#### 1.2 **Cascade 옵션 예시 및 사용 이유**

- 예를 들어, **`SurveyItemOption`** 엔티티에서 **`SurveyItem`**이 삭제될 때 관련된 `SurveyItemOption`도 삭제되어야 합니다. 이를 위해 `CascadeType.ALL` 또는 `CascadeType.REMOVE`를 사용하여 자식 엔티티가 부모 엔티티의 라이프사이클을 따르도록 해야 합니다.

  ```
  java코드 복사@ManyToOne(fetch = FetchType.LAZY, cascade = CascadeType.ALL)
  @JoinColumn(name = "item_id", nullable = false)
  private SurveyItem item;
  ```

  - 이렇게 하면 **연관된 데이터가 자동으로 삭제**되므로 개발자가 모든 관련 데이터를 일일이 삭제할 필요가 없고, 데이터의 무결성도 자연스럽게 유지됩니다.

### 3. **Cascade와 DDL의 `ON DELETE CASCADE`, `ON UPDATE CASCADE` 관계 설명**

`ON DELETE CASCADE`와 `ON UPDATE CASCADE`는 데이터베이스에서의 외래 키 참조 무결성을 관리하기 위한 설정입니다. 이를 **엔티티와 매칭하는 방법**을 설명드리겠습니다.

#### **3.1 `ON DELETE CASCADE`와 `CascadeType.REMOVE/ALL`**

- `ON DELETE CASCADE`

  :

  - 데이터베이스에서 부모 엔티티가 삭제될 때 해당 외래 키를 참조하는 모든 자식 엔티티도 자동으로 삭제되는 기능입니다.
  - **JPA에서 `cascade = CascadeType.REMOVE` 또는 `CascadeType.ALL`**을 설정하면 동일한 동작을 수행합니다. 즉, 부모 엔티티가 삭제될 때 연관된 자식 엔티티도 자동으로 삭제됩니다.
  - 따라서 `ON DELETE CASCADE`와 동일한 역할을 JPA에서도 자동으로 수행할 수 있도록 `CascadeType.REMOVE` 또는 `CascadeType.ALL`을 사용합니다.

#### **3.2 `ON UPDATE CASCADE`와 자동 관리**

- `ON UPDATE CASCADE`

  :

  - 데이터베이스에서 부모 엔티티의 기본 키가 변경되었을 때(예: ID 변경) 그 변경 사항이 자식 엔티티에 반영되어 참조 무결성을 유지합니다.
  - JPA에서 **자동으로 기본 키 업데이트는 잘 일어나지 않으며**(특히 기본 키는 변경하지 않는 것이 일반적입니다), **기본 키 변경이 필요한 경우 직접 수동으로 업데이트**해야 하는 경우가 많습니다. 하지만 **`@ManyToOne` 관계에서 외래 키와 연관된 값이 변경될 경우**는 자식 엔티티의 해당 필드도 업데이트됩니다.

#### **3.3 `cascade = CascadeType.ALL`의 역할**

- `cascade = CascadeType.ALL`

  :

  - 부모 엔티티에 적용된 모든 변경 사항을 자식 엔티티에 자동으로 전파합니다. 여기에는 `PERSIST`, `MERGE`, `REMOVE`, `REFRESH`, `DETACH` 등이 포함됩니다.
  - 이 옵션을 통해, 데이터베이스의 **`ON DELETE CASCADE`**처럼 부모 엔티티가 삭제될 때 자식 엔티티도 함께 삭제되도록 설정할 수 있습니다.
  - 하지만 `ON UPDATE CASCADE`와 직접 매칭되지는 않으며, JPA에서는 외래 키 참조 무결성을 수동으로 관리합니다. 즉, 부모 엔티티의 기본 키 변경이 자식 엔티티에 자동으로 전파되지 않습니다. 대신, 외래 키가 연관된 다른 엔티티의 변경 사항은 관계에 따라 반영될 수 있습니다.

### 2. **Fetch 옵션의 필요성**

**`Fetch`** 옵션은 엔티티 간의 관계를 로딩하는 방식에 대한 설정입니다. 즉, 데이터베이스에서 관계된 데이터를 언제 로딩할지를 결정하는 방식입니다. 이에는 두 가지 주요 유형이 있습니다: `FetchType.EAGER`와 `FetchType.LAZY`.

#### 2.1 **FetchType.LAZY 사용 이유**

- **지연 로딩 (`FetchType.LAZY`)**:

  - 기본적으로 `@ManyToOne` 관계는 **즉시 로딩 (`FetchType.EAGER`)**으로 설정되어 있습니다. 즉시 로딩은 부모 엔티티를 조회할 때 자식 엔티티도 함께 로딩합니다. 하지만 이렇게 하면 부모 엔티티만 필요해도 자식 엔티티가 불필요하게 로딩되어 **성능에 영향을 미칠 수 있습니다**.
  - 반면에 **`FetchType.LAZY`**를 사용하면 부모 엔티티가 로딩될 때 자식 엔티티는 필요할 때만 로딩됩니다. 즉, 부모 엔티티를 조회할 때 실제로 자식 엔티티가 필요하지 않다면 로딩을 지연시키는 것입니다.

  ```
  java코드 복사@ManyToOne(fetch = FetchType.LAZY, cascade = CascadeType.ALL)
  private Survey survey;
  ```

- **성능 최적화**:

  - 데이터베이스의 큰 테이블과 연관된 많은 엔티티가 있을 때, 모든 데이터를 한 번에 로딩하는 것은 많은 메모리를 소비하고 **성능 저하**를 야기합니다. 지연 로딩은 필요할 때만 데이터를 로드함으로써 이러한 문제를 완화할 수 있습니다.
  - 예를 들어 `Survey` 엔티티를 조회할 때 그와 관련된 `SurveyItem`이 수십 개라면, `EAGER`로 모든 데이터를 로드하는 것은 성능 저하를 초래할 수 있습니다. 따라서 `LAZY`를 사용하여 필요할 때만 데이터를 가져오도록 하는 것이 효율적입니다.

#### 2.2 **FetchType.LAZY 적용 예시**

- **양방향 관계에서 사용**:

  - `SurveyVersion`와 `SurveyItem` 간의 관계처럼 **양방향 관계**를 갖는 엔티티의 경우, 두 엔티티 모두 `EAGER`로 설정되어 있으면 **순환 참조**가 발생할 수 있습니다. 예를 들어 `SurveyVersion`을 가져오려고 할 때 `SurveyItem`이 함께 로딩되며, `SurveyItem`은 다시 `SurveyVersion`을 로딩하려고 시도하는 등 무한 순환 문제가 발생할 수 있습니다.

  ```
  java코드 복사@ManyToOne(fetch = FetchType.LAZY, cascade = CascadeType.ALL)
  private SurveyVersion version;
  ```

  - 이 문제를 방지하기 위해 `FetchType.LAZY`를 사용하여 **데이터가 필요할 때만 로딩**하도록 합니다. 이를 통해 순환 참조 문제를 방지하고 성능도 최적화할 수 있습니다.

### 3. **요약**

1. **Cascade 옵션 추가의 이유**:

   - **참조 무결성 보장**: 부모 엔티티가 삭제될 때 자동으로 자식 엔티티들도 삭제되도록 하여 데이터베이스의 참조 무결성을 유지합니다.
   - **개발 편의성**: 부모-자식 관계의 엔티티를 관리하는 데 반복적인 작업을 줄이고, 일관된 라이프사이클 관리를 통해 데이터의 일관성을 유지합니다.

   예를 들어, `SurveyItem`과 `SurveyItemOption` 관계에서 `SurveyItem`이 삭제될 때 관련된 모든 `SurveyItemOption`이 자동으로 삭제되도록 해야 합니다.

2. **Fetch 옵션 추가의 이유**:

   - **성능 최적화**: 불필요한 데이터 로딩을 방지하고 메모리 사용량을 줄임으로써 성능을 최적화할 수 있습니다.
   - **순환 참조 방지**: 양방향 관계에서 순환 참조로 인한 무한 로딩을 방지하여 성능 문제를 피할 수 있습니다.

   예를 들어, `SurveyVersion`과 `SurveyItem` 간의 관계에서 지연 로딩(`FetchType.LAZY`)을 통해 `SurveyItem`이 필요할 때만 로딩되도록 설정하여 성능을 최적화할 수 있습니다.

이렇게 각 설정을 적용하면 엔티티와 데이터베이스 간의 일관성이 유지되고, 성능과 무결성을 보장하는 안전한 설계를 유지할 수 있습니다.