
### 자바의 명명 규칙: 철자와 문법

자바의 명명 규칙은 **철자 규칙**과 **문법 규칙**으로 나뉜다.


## 철자 규칙

**1. 패키지**
- 패키지와 모듈 이름은 계층적으로 짓고, 각 요소를 점(`.`)으로 구분한다.
- 요소는 **소문자 알파벳**과 드물게 **숫자**로 구성된다.
- 조직 외부에서 사용할 패키지는 도메인 이름을 역순으로 사용한다. (예: `com.google`)
    - `java`는 표준 라이브러리, `javax`는 선택적 패키지를 나타낸다.
- 패키지 이름의 각 요소는 일반적으로 8자 이하로 짧게 쓴다.
    - 예: `utilities`보다는 `util`이 추천된다.
    - 여러 단어로 구성된 이름은 약어 형태(예: `awt`)로 써도 된다.
- 인터넷 도메인 이름 뒤에 요소 하나만 붙이는 단순 패키지가 많으나, 많은 기능을 제공한다면 계층적으로 나눌 수 있다.
    - 예: `java.util.concurrent.atomic` (하위 패키지).

**2. 클래스와 인터페이스**
- 클래스와 인터페이스 이름은 하나 이상의 단어로 구성되며, 첫 글자는 **대문자**로 시작한다.
- 가능한 한 단어를 줄여 쓰지 않는다. (통용되는 약어는 예외: `HttpUrl`)
- 약어도 첫 글자만 대문자로 하는 형태가 읽기 쉽다.
    - 예: `HttpUrl` (대문자 전체 약어 `HTTPURL`은 피한다).

**3. 메서드와 필드**
- 메서드와 필드 이름은 첫 글자를 소문자로 시작하는 것을 제외하면 클래스 이름과 동일한 규칙을 따른다.
- 첫 단어가 약어라면 전체를 소문자로 쓴다.
    - 예: `urlParser`, `httpClient`.
- 상수 필드(`static final`) 이름은 **모두 대문자**로 쓰며, 단어는 밑줄(`_`)로 구분한다.
    - 예: `MAX_BUFFER_SIZE`.
- 지역 변수는 약어를 써도 괜찮다. 문맥상 유추하기 쉽기 때문이다.
    - 예: `i`, `denom`, `hostNm`.
- **입력 매개변수**는 지역 변수와 비슷하지만, 메서드 설명 문서에도 등장하므로 더 명확한 이름을 사용하는 것이 좋다.
- **타입 매개변수**는 보통 한 글자로 표현한다.
    - `T`: 임의의 타입
    - `E`: 컬렉션 원소 타입
    - `K`, `V`: 맵의 키와 값
    - `X`: 예외 타입
    - `R`: 메서드 반환 타입
    - 복수 타입에는 `T`, `U`, `V`를 사용한다.

---

## 문법 규칙

**1. 패키지 이름**
- 특별한 문법 규칙은 없다.

**2. 클래스 이름**
- **단수 명사** 또는 **명사구**로 짓는다.
    - 예: `Thread`, `PriorityQueue`.
- 객체를 생성할 수 없는 클래스라면 **복수형 명사**를 사용한다.
    - 예: `Collectors`, `Collections`.
- 인터페이스 이름은 클래스와 동일하게 짓거나, `able` 또는 `ible`로 끝나는 **형용사**를 사용한다.
    - 예: `Runnable`, `Iterable`.
- 애너테이션 이름은 명사, 동사, 형용사 등 다양하게 쓸 수 있다.
    - 예: `Inject`, `ImplementedBy`, `Singleton`.

**3. 메서드 이름**
- **동작을 수행하는 메서드**는 **동사**나 **목적어 포함 동사구**로 짓는다.
    - 예: `append`, `drawImage`.
- `boolean` 값을 반환하는 메서드는 **is~** 또는 **has~**로 시작하며, **명사구**나 **형용사**로 끝난다.
    - 예: `isEmpty`, `hasChildren`.
- 반환 타입이 `boolean`이 아니거나 인스턴스 속성을 반환한다면 **명사** 또는 **명사구**로 짓는다.
    - 예: `size`, `getSize`.
    - `get~` 형태만 고집할 필요는 없다. 간결한 형태가 더 읽기 쉽다면 사용한다.
        - 예: `car.speed()`.
- **타입을 변환**하는 메서드는 보통 `toType` 형태로 짓는다.
    - 예: `toString`.
- **다른 뷰를 반환**하는 메서드는 `asType` 형태로 짓는다.
    - 예: `asList`.
- **기본 타입 값을 반환**하는 메서드는 `typeValue` 형태로 짓는다.
    - 예: `intValue`.
- **정적 팩터리 메서드**의 이름은 다양하며, 다음과 같은 패턴을 자주 사용한다.
    - `of`, `from`, `valueOf`, `instance`, `getInstance`, `create`, `newInstance`.

**4. 필드 이름**
- 필드 이름에 대한 문법 규칙은 중요도가 낮다.
- API 설계가 적절하다면, 필드가 외부에 노출될 일이 거의 없기 때문이다.

---

### 결론
- 표준 명명 규칙을 체화하며 자연스럽게 쓸 수 있게 하자.
- 철자 규칙은 직관적이지만, 문법 규칙은 복잡하고 느슨하다.
- 상식이 이끄는대로 따르자.