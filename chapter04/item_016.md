# 아이템 16. public 클래스에서는 public 필드가 아닌 접근자 메서드를 사용하라

<br>

## 캡슐화의 이점을 제공하지 못하는 클래스
데이터 필드에 직접 접근하여 수정이 가능하다. 따라서 `캡슐화의 이점`을 제공하지 못한다.

```java 

class Point {
    public double x;
    public double y;
}

```

<br>

## 객체 지향 방식으로 캡슐화 한 클래스
필드들을 모두 `private`으로 변경
public `접근자(getter)`, `변경자(setter)` 추가

```java

class Point {
    private double x;
    private double y;

    public Point(double x, double y){
        this.x = x;
        this.y = y;
    }

    public double getX(){
        return this.x;
    }

    public double getY(){
        return this.y;
    }

    public void setX(double x){
        this.x = x;
    }

    public void setY(double y){
        this.y = y;
    }
}

```
이렇게 패키지 바깥에서 접근할 수 있는 클래스라면 접근자를 제공함으로써 클래스 내부 변경을 유연하게 한다.
`package-priavte` 클래스 혹은 `private` 중첩클래스라면 데이터 필드를 노출한다 해도 문제가 되지 않는다.

<br>

## 자바 플랫폼 라이브러리에서 필드를 노출시킨 사례
자바플랫폼 라이브러리에도 public 클래스의 필드를 직접 노출하지 말라는 규칙을 어긴 사례가 종종 있다.
대표적인 예로 java.awt 의 Point, Dimension 클래스이다.

```java

public class Point extends Point2D implements java.io.Serializable {
    /**
     * The X coordinate of this <code>Point</code>.
     * If no X coordinate is set it will default to 0.
     *
     * @serial
     * @see #getLocation()
     * @see #move(int, int)
     * @since 1.0
     */
    public int x;

    /**
     * The Y coordinate of this <code>Point</code>.
     * If no Y coordinate is set it will default to 0.
     *
     * @serial
     * @see #getLocation()
     * @see #move(int, int)
     * @since 1.0
     */
    public int y;

    /*
     * JDK 1.1 serialVersionUID
     */
    private static final long serialVersionUID = -5276940640259749850L;
}
```
이렇게 public으로 클래스 필드를 선언하면 문제가 된다.

<br>

## 불변 필드를 public으로 선언

```java

public final class Time {
	private static final int HOUR_PER_DAY = 24;
	private static final int MINUTES_PER_HOUR = 60;

	public final int hour;
	public final int minute;

	public Time(int hour, int minute){
		if (hour < 0 || hour >= HOUR_PER_DAY)
			throw new IllegalArgumentException("시간 : "+hour);
		if (minute < 0 || minute >= MINUTES_PER_HOUR)
			throw new IllegalArgumentException("분 : "+minute);

		this.hour = hour;
		this.minute = minute;

	}
}

```

<br>

## 정리
public 클래스는 절대 `가변 필드`를 직접 노출해서는 안 된다. - 블로크

불변 필드라면 안심할 수는 없지만 노출해도 된다 생각한다. (설계상 필요하다면) - 김선용

하지만 `package-private` 클래스나 `private` 중첩 클래스에서는 종종 (`불변이든 가변이든`)필드를 노출하는 편이 나을 때도 있다. - 어떤 작자 미상
