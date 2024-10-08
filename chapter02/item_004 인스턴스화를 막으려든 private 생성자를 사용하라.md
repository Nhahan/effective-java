개발을 하다보면 수학 계산이나 유틸리티같은 도우미 클래스 처럼 주로 정적 메서드와 정적 필드로만 이루어진 클래스를 생성하게 된다. 물론 객체 지향적이진 않지만 굉장히 도움이 되는 순간들이 많다.

주로 이러한 정적 필드와 정적 메서드로만 이루어진 클래스들은

- 유틸리티 함수
- 상수 관리
- 상태없는 메서드 (그러니까 순수함수의 기능만을 제공하는)
- 팩토리 메서드 패턴
- final 클래스와 관련한 메서드들을 모아 놓을때

이러한 클래스들은 그 자체로 인스턴스의 상태를 가지지 않기 때문에, 어디서든지 일관성 있는 동작을 기대할 수 있다.

팩토리 메서드 패턴을 조금 간략하게 설명하자면

이런식으로 외부에서 호출할때 type만 넘기고 구체적인 클래스는 몰라도 객체요청을 할 수 있도록 유연성을 높이는 패턴을 말한다.

```python
class VehicleFactory {
    public static Vehicle getVehicle(String type) {
        if (type == null) {
            return null;
        }
        if (type.equalsIgnoreCase("CAR")) {
            return new Car();
        } else if (type.equalsIgnoreCase("TRUCK")) {
            return new Truck();
        }
        return null;
    }
}

```

여튼 이런 정적 멤버만 담은 클래스는 인스턴스로 만들어 쓰려고 설계한 게 아니다. 그러나 생성자를 명시하지 않으면 컴파일러는 자동으로 기본 생성자를 만든다. 사용자는 이에 대해 생성자가 자동 생성된 것인지 구분 할 수 없을 뿐더러 예상치 못한 동작이기 때문에 좋지 않다.

그러면 추상 클래스로 만들어 인스턴스화를 막을 수 있을까? 물론 그것만으로는 힘들다.. 추상 클래스 또한 하위클래스로 만들어 인스턴스화 하면 그만이기 때문이다.(그리고 추상화로 만들어 뒀을때 히스토리를 모르는 사람은 상속해서 쓰라고 오해할수도 있으니 되려 문제다!)

그렇다면 이러한 정적(필드와 메서드만 쥐고있는..) 클래스는 인스턴스화를 어떻게 막을까? 컴파일러가 기본 생성자를 만드는 경우는 명시된 생성자가 없을때니까 **private 생성자를 추가하면 클래스의 인스턴스화를 막을 수 있다.**

```java
// 인스턴스를 만들 수 없는 유틸리티 클래스
public class Utility{
	private Utility(){
	// 기본 생성자가 만들어지는 것을 막기(인스턴스 방지)
		throw new AssertionError();
	}
}
```

이렇게 두면 명시적 생성자가 private이니 클래스 바깥에서는 접근이 불가능하다.

private인데도 추가적으로 호출됐을때 에러를 던지는 이유는 히스토리를 모르는 또다른 개발자가 클래스 내부에서 호출하게 되는 불상사를 막기 위함이다.

그러나 생성자가 분명 존재하는데 어떻게든 호출을 막으려는 모양새가 직관적이진 않기때문에 주석을 달아두는 것이 좋다.

또한 이렇게 만들어두면 상속이 불가능해지기도 한다. 상속 받게 되면 하위클래스는 어떻게든 상위 클래스의 생성자를 호출하게 될텐데, private으로 선선했기에 하위 클래스가 접근하는 케이스도 고려한 셈이다.