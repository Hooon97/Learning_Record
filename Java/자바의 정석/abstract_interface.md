# Abstract Class 추상 클래스
추상 클래스는 미완성 메서드를 포함한 메서드를 의미한다. 미완성이라는 말은, 메서드의 **선언부만 작성**하고 **구현부는 작성하지 않는 것**을 말한다.</br>
`abstract` 키워드로 추상 클래스임을 명시할 수 있다. 미완성 메서드는 해당 추상 클래스를 상속 받는 자손 클래스에서 완성된다. 이 때 주의해야 할 점은, 자손 클래스에서 **미완성 메서드**는 **반드시 오버라이딩**을 통해 완성되어야 한다는 점이다.</br>
또한 추상 클래스는 자신만의 메서드와 멤버 변수를 가질 수 있다. 그리고 추상 메서드가 없어도 `abstract` 키워드를 적으면 추상 클래스로 취급한다.

예시 코드는 아래와 같다.
```
abstract class Human {
    int age;
    abstract void eat();
    abstract void sleep(String time);
    abstract boolean wakeup();
}
```

`eat()`, `slepp()`, `wakeup()` 메서드가 추상 메서드다. 추상 메서드는 메서드 앞에 `abstract` 키워드가 붙는다. 해당 추상 클래스를 상속 받으면 아래와 같이 적을 수 있다.

```
class Parent extends Human{
    void eat(){
        System.out.println("밥 먹는 중");
    }

    void sleep(String time){
        System.out.println(time+"에 잡니다.");
    }

    boolean wakeup(){
        System.out.println("일어납니다.");
        return true;
    }

}
```
물론 `Parent` class는 자기 자신만의 메서드도 가질 수 있다.</br>

추상 클래스를 사용하는 이유는, 기존 클래스들의 공통적인 부분을 하나로 묶을 수 있기 때문이다. `Human` 클래스를 상속받을 수 있는 클래스는 다양하다. `Parent`, `Child`, `Man`, `Woman`, `Teacher`, `CEO`... 셀 수 없이 많다. 이 때 여러 클래스들이 공통적으로 가지고 있는, 사람으로서 할 수 밖에 없는 특징과 행동을 abstract로 묶어 놓으면 코드 관리가 용이할 것이다.</br>
그냥 `class`로 선언하지 않고 `abstract`로 선언한 것은, 사람마다 **행동**은 동일하지만 **행동의 구현**은 다른 방식이기 때문이다. 이를테면 사람마다 `eat()`의 구현, 즉 먹는 방식은 제각각이다.</br>
또 한가지 이점이 있는데, 동일한 추상 클래스를 상속받은 클래스의 인스턴스들은 **다형성**에 의하여 하나의 배열에 담길 수 있다.</br>
```
Human[] human_races = new Human[4];
human_races[0] = new Parent();
human_races[1] = new Child();
human_races[2] = new Teacher();
human_races[3] = new CEO();

for(int i = 0; i<4; i++){
    human_races[i].eat();
}
```
</br>

# Interface 인터페이스
인터페이스는 일종의 추상 클래스로, 추상 클래스가 메서드와 멤버 변수를 가질 수 있었다면 인터페이스는 가질 수 없다. 즉, 오직 **추상 메서드**와 **상수**만을 가진다.</br>
키워드는 `interface`로, 일반 클래스에서 인터페이스 클래스를 `구현`할 땐 `implements`로 받을 수 있다. `상속`과 유사하다.</br>
인터페이스는 여러 특징이 있다.

1. 인터페이스는 인터페이스로부터만 상속받을 수 있다.
2. 다중 상속을 허용한다.
3. 모든 멤버 변수는 `public static final`이 붙어 상수다.
4. 모든 메서드는 `public abstract`이다.
5. 모든 인터페이스의 공통 사항이기 때문에, 생략이 가능하고, 생략 시 컴파일러가 자동으로 생성한다.
6. `Object` 클래스를 상속하지 않는다.

```
interface Movable{
    void move(int x, int y);
}

interface Attackable{
    void attack(Human h);
}

interface Huntable extends Movable, Attackable{

}
```
이 때 `Huntable` 인터페이스 클래스는 `Movable`의 `move()` 메서드와 `Attackable`의 `attack(Human h)` 메서드를 모두 상속받아 가지고 있다.</br>

인터페이스도 일종의 추상 클래스이므로 인터페이스를 구현받은 일반 클래스들은 인터페이스의 추상 메서드를 모두 구현해야 한다. 만약 모두 구현하지 않는다면, `abstract`를 사용하여 추상 클래스로 바꿔주어야 한다.</br>

## 인터페이스를 이용한 다형성
추상 클래스에서 **다형성**이 적용 되었듯이, 인터페이스에도 **다형성**이 적용된다. 이 말은, 인터페이스를 구현한 클래스는 해당 인터페이스의 자손 클래스로 취급하고, 따라서 해당 인터페이스 타입의 참조 변수는 구현한 클래스의 인스턴스를 참조할 수 있다는 말이다.</br>

다음과 같은 클래스가 있을 때, `Hunter` 클래스는 `Huntable` 인터페이스를 구현하고 있다. 이 때 `Hunter` 인스턴스를 `Huntable` 참조변수가 참조하는 것이 가능하다.
```
class Hunter extends Human implements Huntable{
    void move(int x, int y){
        // 움직이는 로직
    }
    void attack(Human h){
        // 사냥하는 로직
    }

}
```
```
Huntable h = new (Huntable)Hunter();
Huntable h2 = new Hunter();
```
이러한 특성으로 메서드에서 매개변수로 인터페이스를 넣는 것도 가능하다. 단, 매개 변수로 입력된 인터페이스는 해당 인터페이스를 구현한 `클래스의 인스턴스`를 반환한다. 예로 들면 다음과 같다.
```
void hunt(Huntable h){

}
```
```
void hunt(Hunter h){
    // 사냥하는 로직
}
```
두 메소드는 결과적으로 같다.</br>
마찬가지로, 리턴 타입이 인스턴스인 경우에는 해당 인스턴스를 구현한 클래스의 인스턴스를 반환시켜야 한다.

## 인터페이스를 사용하면 장점

1. 개발 시간 단축
2. 표준화가 가능하다.
3. 관계없는 클래스들끼리 관계를 맺어줄 수 있다.
4. 독립적인 프로그래밍이 가능하다.

클래스의 선언과 구현을 분리시킨다는 것은 특정 데이터베이스에 종속되지 않는다는 것을 의미한다.
