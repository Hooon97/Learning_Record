# Constructor 생성자
생성자는 **인스턴스 초기화 메서드**이다. 인스턴스가 생성될 때 인스턴스 변수를 초기화 하거나, 사용자가 정의한 인스턴스 생성 시 수행되어야 할 일련의 작업들을 설정해놓을 수 있다.</br>

`home`이라는 객체를 생성한다고 해보자. 이 때 객체를 생성하는 방식은 다음과 같았다.
```
home myHome = new home();
```
`myHome`은 `new` 연산자로 호출된 `home()` 생성자의 주소 값을 저장한다. 즉, 연산자 `new`가 Heap 메모리에 home 클래스의 인스턴스를 생성하면, 생성자 `home()`이 호출되어 수행된다. 또한 `new`의 결과로 `home`의 인스턴스 주소가 반환되어 참조변수 `myHome`에 저장된다.

</br>

일반적인 메서드와 유사하지만 인스턴스를 초기화 한다는 특별한 설정으로, 몇가지 특이점이 있다.</br>

1. 리턴 타입과 리턴이 없다.
2. 생성자의 이름은 클래스의 이름과 같다.

예를 들면 아래와 같다.
```
class home{
    int price;
    String adress;
    int capability;

    // 1
    home(){}
    
    // 2
    home(int price){
        this(price, "Seoul", 2);
    }
    
    // 3
    home(int myPrice, String myAdress, int capa){
        price = myPrice;
        adress = myAdress;
        capability = capa;
    }
}
```

`home()`, `home(int price)`, `home(int myPrice, String myAdress, int capa)` 모두 생성자다.</br>

생성자에는 **기본 생성자**와 **매개 변수를 포함한 생성자**, **생성자를 포함한 생성자**가 있다.

</br>

## 기본 생성자
기본 생성자는 사용자가 클래스 내에 생성자를 정의하지 않았을 때에 컴파일러가 자동적으로 생성해준다. 위의 예시에서 `home() {}`에 해당하며, 메소드 내부에 아무런 값이 없기 때문에 아무런 작업을 하지 않는다.

## 매개 변수를 포함한 생성자
매개 변수를 포함한 생성자는 인스턴스를 생성할 때 정의된 코드를 따라 멤버 변수를 초기화 된 상태로 인스턴스 객체를 생성하도록 한다. 위의 예시에서는 `home(int price)`가 그 예시다. `int price`가 매개변수로 생성자에 들어가있다.</br>

이 생성자 내부에는 `this(price, "Seoul", 2)`가 있다. 생성자 내부에 생성자를 호출할 경우 `this()`를 통해 호출할 수 있다. 이번 경우에서 생성자 내부에서 호출된 생성자는 3번 생성자다. 즉, 사용자가 2번 형태의 생성자로 인스턴스를 생성할 경우 `price`에는 사용자가 입력한 값이, `adress`에는 "Seoul"이, `capability`는 2로 멤버 변수들이 초기화되는 것이다.

## this와 this()의 차이
`this`는 참조 변수로 자기 자신을 가리킨다. `this()`는 생성자를 가리킨다. 단, `this()`는 생성자 내부에서만 사용될 수 있다.</br>
만약 매개 변수를 받는 생성자에서, 매개 변수의 이름과 클래스가 지닌 멤버 변수의 이름이 같으면 컴파일러 입장에서는 둘을 구분할 수 없다. 이 때 `this.price`는 클래스의 멤버 변수 `price`를 의미하고, `price`는 생성자의 매개 변수로 입력된 변수임을 의미한다.

## 인스턴스 복사
이미 생성되고 멤버 변수들이 정의된 인스턴스를 복사할 경우가 있다면, 생성자를 이용하면 편리하다. 생성자가 다음과 같이 정의되어 있으면 아래와 같이 인스턴스르 복사할 수 있다.
```
class home{
    int price;
    String adress;
    int capability;

    home(){
        price = 12;
        adress = "Seoul";
        capability = 4;
    }

    home(home a){
        price = a.price;
        adress = a.adress;
        capability = a.capability;
    }
}
```
```
home myHome = new home();
System.out.println(myHome.price); // 12

home cloneHome = new home(myHome);
System.out.println(cloneHome.price); // 12

myHome.price = 30;
System.out.println(myHome.price); // 30
System.out.println(cloneHome.price); // 12
```
단, 두 인스턴스는 개별 메모리 공간에서 관리되므로 하나의 인스턴의 멤버 변수 값이 변화되어도 다른 인스턴스는 영향을 받지 않는다.</br>

Java는 객체를 복사할 수 있는 여러 API를 제공하고 있다. `clone`도 그 중 하나이다.

</br>

# 변수 초기화
변수를 선언하고 처음 값을 정해주는 것을 `변수의 초기화`라고 한다. 경우에 따라서 필수적일수도, 아닐수도 있지만 선언과 동시에 적절한 값으로 초기화 해주는게 좋을 것이다.</br>

멤버 변수는 따로 초기화를 해주지 않아도 변수의 자료형에 맞도록 알아서 초기화가 된다. 이를테면 `int`형 변수는 `0`이 기본 값이다. 그러나 지역 변수는 반드시 **초기화 과정을 거쳐야** 사용할 수 있다.

멤버 변수의 초기화에는 세 가지 방법이 있다.

1. 명시적 초기화 (Explicit Initialization)
2. 생성자를 이용한 초기화 (Constructor)
3. 초기화 블록을 이용한 초기화 (Initialization Block)
    - 인스턴스 초기화 블록 : 인스턴스 변수 초기화
    - 클래스 초기화 블록 : 클래스 변수 초기화

## 명시적 초기화 (Explicit Initialization)
가장 간단하고 기본적이다. 선언과 동시에 초기화하는 것이다.
```
class home{
    int price = 12; // 기본형 변수 초기화
    Owner owner = new Owner(); // 참조형 변수 초기화
}
```

## 생성자 (Constructor) 초기화
이는 생성자에서 이미 다뤘던 내용이다.</br>
생성자는 인스턴스의 멤버 변수들을 초기화하는데 사용된다.

## 초기화 블록 (Initialization Block)
초기화 블록은, 초기화 작업이 복잡해서 명시적 초기화로 초기화가 어려울 경우 활용한다. 초기화 블록 내에는 조건문, 반복문, 예외 처리 등을 실행 시킬 수 있기 때문이다.</br>

단순히 `{}`을 작성함으로 초기화 블록을 활용할 수 있고, 클래스 내에 블록{}을 작성하고 블록 내에 코드를 작성하면 `인스턴스 초기화`를 할 수 있다. 만약 블록 앞에 `static`을 붙이면, `클래스 초기화 블록`이 된다.</br>

1. 클래스 초기화 블록은 클래스가 메모리에 처음 로딩될 때 한 번만 실행되며, 
2. 인스턴스 초기화 블록은 생성자와 같이 인스턴스를 생성할 때 마다 수행된다.
3. 인스턴스 블록은 생성자보다 먼저 실행된다.

따라서 인스턴스 변수의 초기화는 주로 생성자를 통해 선언되며, 생성자에서 공통적으로 수행되는 코드는 인스턴스 블록으로 처리할 수 있다.</br>
예를 들어, 다음과 같은 코드는 초기화 블록을 이용해 아래와 같이 축약될 수 있다.
```
    home(){
        count++;
        serialNo = count;
        price = 12;
        adress = "Seoul";
        capability = 4;
    }

    home(home a){
        count++;
        serialNo = count;
        price = a.price;
        adress = a.adress;
        capability = a.capability;
    }
```
```
{
    count++;
    serialNo = count;
}

home(){
        price = 12;
        adress = "Seoul";
        capability = 4;
    }

    home(home a){
        price = a.price;
        adress = a.adress;
        capability = a.capability;
    }
```
**코드의 중복을 제거**하면 **코드의 신뢰성이 높아**지고, **오류 발생 가능성**을 줄인다.</br>
다른 말로 하면 **재사용성**을 높이고 **중복을 제거**하여 객체지향 프로그래밍의 철학을 반영할 수 있다.</br>

마지막으로 중요한 부분이 남았다. 멤버 변수를 초기화 하는 방법이 조건에 따라 3가지가 있는 걸 알겠는데, 초기화 순서를 제대로 숙지하지 않으면 애써 설계한 코드를 처음부터 다시 짜야 할지도 모른다. 애초에 컴파일이 안 될 확률이 높다.</br>

1. 클래스 초기화가 인스턴스 초기화보다 빠르다.
2. 클래스 초기화 내에서, </br>
**기본값 -> 명시적 초기화 -> 클래스 초기화 블록**</br>
순서로 초기화가 진행된다.
3. 인스턴스 초기화 내에서, </br>
**기본값 -> 명시적 초기화 -> 인스턴스 초기화 블록** -> 생성자</br>
순서로 초기화가 진행된다.

즉, </br>
클래스 초기화 > 인스턴스 초기화</br>
기본 값 > 명시적 초기화 > 초기화 블록 > 생성자</br>
순서로 진행된다.