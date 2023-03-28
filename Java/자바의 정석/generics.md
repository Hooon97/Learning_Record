# Generics 지네릭스
다양한 타입의 객체들을 다루는 메서드나 컬렉션 클래스에 **컴파일 시의 타입 체크**를 해주는 기능이다. 다시 말해 객체의 타입을 미리 명시해줌으로써 형변환을 줄여주는 기능이다. </br>이를 통해 객체의 **타입 안정성**을 높이고, **형변환의 번거로움**을 줄여준다.</br>
예를 들어 `ArrayList`는 다양한 종류의 객체를 담을 수 있지만, 보통 한 종류의 객체를 담는다. **제네릭스**를 활용하면 담을 수 있는 객체의 종류가 한정되어, 객체를 꺼낼 때 마다 형변환하거나 접근이 금지된 객체가 담기는 경우를 방지해준다.</br>
`T` 문자를 주로 활용하는데, 예시는 아래와 같다. 물론 `K`나 `V`, `S`도 가능하다. Java 문서를 보면 `Map<K, V>`로 설명이 적혀있는 걸 볼 수 있다.
```
class Box<T>{
    T item;

    void setItem(T item){this.item = item;}
    T getItem(){return item;}
}
```
`Box<Object>`와 `Box<T>`는 비슷하지만, `Object`가 입력되는 경우 어떤 종류의 객체든 담길 수 있지만, `<T>`의 경우 사용자가 지정한 종류의 객체만 가능하다. 예를 들어 아래와 같다.
```
Box<Apple> b = new Box<Apple>(); // Apple 객체를 받는다.
b.setItem(Grape); //안된다.

// Box<Apple> b_test = new Box<Grape>(); //안된다.
```
현재 자바는 지네릭스가 적용된 상태기 때문에 익숙하고 당연할 수 있는데, 지네릭스의 적용으로 더 간편해졌다고 보며 된다. JDK 1.7 이 후 부터는 더 간소화되어, 다음과 같이 생략이 가능하다.
```
Box<Apple> b = new Box<>();
```
어차피 `Apple` 객체만 입력 가능하니까 생략하는 것이다.</br></br>

## 지네릭스의 사용 제한
단, `static` 메서드, 멤버 변수에는 사용이 불가능하다. 지네릭스는 인스턴스 변수로 간주되기 때문이다. `static` 멤버는 타입 변수에 지정된 타입, 대입된 타입의 종류에 관계없이 동일한 것이어야 하기 때문이다.</br>
지네릭 배열을 만드는 것도 안된다. 이는 `new`연산자 때문으로, 이 연산자는 컴파일 시점에서 `T`가 무엇인지 정확하게 알아야 하기 때문이다.
```
T[] tmpArr = new T[10]; //안된다.
```

## 지네릭 클래스의 객체 생성과 사용
대신 아래처럼 지네릭 클래스의 객체 배열은 생성이 가능하다.
```
ArrayList<String> tmpArr = new ArrayList<String>();

Box<Fruit>[] fruitBox = new Box<Fruit>[10];
```
지네릭 클래스와 상속 관계에 있는 클래스들은 다형성이 적용되기도 한다. 만약 `Fruit` 클래스가 `Apple` 클래스와 `Grape` 클래스의 조상 클래스라면,
```
fruitBox[0] = new Apple(); // 된다.
fruitBox[1] = new Grape(); // 된다.
fruitBox[2] = new Fruit(); // 된다.
// fruitBox[3] = new Car(); //안된다.
```
제네릭스를 사용하면 타입 문자로 사용할 타입을 명시하면 한 종류의 타입만 저장할 수 있도록 제한할 수 있다. 하지만 사용자는 여전히 모든 종류의 객체를 지정할 수 있다. 이 때 `extends`를 이용하면, **타입 매개변수 T**에 지정할 수 있는 **타입의 종류를 제한**할 수 있다.</br>
타입 매개변수 `T`가 `Fruit`로 확장되어, 해당 클래스 계열(자손 관계에 있는) 클래스만 담을 수 있게 되었다.
```
class FruitBox(T extends Fruit){ }
```
```
// FruitBox<Car> fruitBox = new FruitBox<Car>(); // 안된다.
FruitBox<Apple> fruitBox = new FruitBox<>(); //된다.
```
여러 클래스로 확장하고 싶다면 `&` 연산자를 이용하면 된다.
```
class FruitBox(T extends Fruit & Meat) { }
```

## 와일드 카드
`static` 메서드에는 지네릭스를 적용할 수 없었다. 그럼 다음과 같은 경우엔 어떻게 해야할까?</br>
`Jucier` 클래스는 
1. 지네릭 클래스가 아니고 
2. static 메서드는 타입 매개변수를 받을 수 없다.
```
class Jucier{
    static Juice makeJuice(FruitBox<Fruit> Box){
        String tmp = "";
        for(Fruit f : box.getList()) tmp += f+"";
        return new Juice(tmp);
    }
}
```
이런 상황에서 `FruitBox`는 지네릭 클래스로 자손 타입의 객체들을 저장할 수 있지만, 이와 연관된 `Jucier` 클래스는 그럴 수 없다.
```
FruitBox<Fruit> fruitBox = new FruitBox<Fruit>();
FruitBox<Apple> appleBox = new FruitBox<Apple>();

Jucier.makeJuice(fruitBox); // 가능
Jucier.makeJuice(appleBox); // 불가능
```
왜 `makeJuice(FruitBox<Fruit>)`메서드는 매개변수 타입을 이미 지정했다. 따라서 `appleBox`는 매개변수로 입력될 수 없다. 그렇다면 자손의 종류별로 메서드를 모두 만들어야 할까?
```
static Juice makeJuice(FruitBox<Fruit> Box){
        String tmp = "";
        for(Fruit f : box.getList()) tmp += f+"";
        return new Juice(tmp);
}

static Juice makeJuice(FruitBox<Apple> Box){
        String tmp = "";
        for(Apple a : box.getList()) tmp += f+"";
        return new Juice(tmp);
}
    
```
이렇게 작성하면, 매개변수 타입이 다르므로 `오버라이딩`이 될 수 있을 것이다. **아니다.** 안된다.</br>
`FruitBox`는 지네릭 클래스로, 지네릭 타입은 컴파일러가 컴파일을 할 때만 사용하고 이 후 제거한다. 따라서, 위의 메서드들은 오버라이딩된 제각각의 메서드가 아니고, 그냥 중복 정의된 것이다.</br>
이를 해결하기 위해 고안된 것이 `와일드 카드`이다. `?`

> `<? extends T>` 와일드 카드 상한 제한, T와 그 자손들만 가능하다.</br>
> `<? super T>` 와일드 카드 하한 제한, T와 그 조상들만 가능하다.</br>
> `<? extends Object>`, `<?>` 모든 타입 가능

사용법도, 제한법도 제네릭과 비슷하다. 위의 예시를 와일드카드를 사용해 설계해보자.

```
static Juice makeJuice(FruitBox<? extends Fruit> Box){
        String tmp = "";
        for(Fruit f : box.getList()) tmp += f+"";
        return new Juice(tmp);
}
```
이제 다음과 같이 사용이 가능하다.
```
FruitBox<Fruit> fruitBox = new FruitBox<Fruit>();
FruitBox<Apple> appleBox = new FruitBox<Apple>();

Jucier.makeJuice(fruitBox); // 가능
Jucier.makeJuice(appleBox); // 가능
```

## 지네릭 메서드
메서드 선언부에 지네릭 타입이 선언된 메서드다.</br>
아래 코드는 `Collections.sort()`이다.
```
static <T> void sort(List<T> list, Comparator<? extends T> c)
```
이제 `makeJuice` 메서드를 지네릭 메서드로 바꿔보자.
```
static <T extends Fruit> Juice makeJuice<FruitBox<T> box) {
    String tmp = "";
        for(Fruit f : box.getList()) tmp += f+"";
        return new Juice(tmp);
}
```
~~이처럼 지네릭 메서드는 매개 변수에 지네릭, 와일드 카드가 적용될 때 좀 더 간편하게 쓰고자 고안된 방법이라고 이해했다. 하지만 정확한지는 모르겠다.~~