# Overloading 오버로딩 
> </br>같은 이름을 가진 여러 메서드가 존재할 수 있다. </br></br>

 메서드는 서로 다른 이름을 가져야 하지만, 메서드의 매개 변수의 개수 혹은 타입, 순서가 다르면 메서드의 이름을 재활용 할 수 있다.</br>

메서드 오버로딩을 할 수 있으면 두 가지 장점이 있다.

1. 메서드의 이름을 아낄 수 있다.
2. 비슷한 기능을 하는 여러 메서드들의 이름을 통일시킨다.

메서드 오버로딩이 되려면 다음의 두 가지 조건이 필요하다.

1. 메서드의 **이름이 같다**.
2. 매개변수의 **개수 또는 타입이 달라야** 한다.

 </br>
 오버로딩(Overloading)은 사전적 의미로 '과적하다'라는 뜻을 가지고 있다. 같은 이름의 다른 메서드가 여러 개 존재할 수 있는 Java의 문법적 규칙과 일맥상통하다.</br>
 아래 예시로 메서드 오버로딩이 적용된 사례와 그렇지 않은 경우를 구분할 수 있다.
 
 ```
 class test{
  public int add(int a, int b) {return a+b;} // 1
  public int add(long a, int b) {return a+b;} // 2
  public long add(int a, int b) {return a+b;} // 3
  public long add(int[] a) {return 배열의 합;} // 4
 }
 ```
이 때 1,2,4의 경우는 서로 오버로딩 되었다고 할 수 있다. 하지만 3번은 1번과 동일한 메서드로 취급된다. `반환타입`은 오버로딩의 조건이 아니다. 오버로딩은 `매개 변수의 타입`과 `매개 변수의 개수`로 구분될 수 있다.

 ## 가변인자
></br>
>메서드에 입력되는 매개 변수의 개수를 동적으로 설정할 수 있다.
></br></br>
</br>
가변 인자의 등장으로 메서드 구현이 더 간편해졌다. 예를 들어 아래와 같던 메서드가

```
    int add(int a){return a}
    int add(int a, int b){return a+b}
    int add(int a, int b, int c){return a+b+c}
    int add(int a, int b, int c, int d) {return a+b+c+d}
```
가변 인자를 활용하면 아래처럼 하나로 축약 가능하다.
```
    int add(int...a){
        int result = 0;
        for(int num : a){
            result += num;
        }
        return num;
    }
```
메서드 내부를 살펴보면 알겠지만 `int...a`가 가변인자의 표현 방식이고, 가변 인자는 배열의 형태로 활용된다. 매개 변수를 여러개 넣어도 가능하다. 단, 이 때는 가변 인자를 가장 마지막에 선언해줘야 한다. 아래와 같다.

```
    int add(int a, int...b){
        //내부 동작
    }
```
가변 인자로 구현된 메서드는 `오버로딩`할 때 주의해야 한다. 메서드를 호출할 때 컴파일러가 구분하지 못할 수 있기 때문이다. 위의 예시로 들었던 `add` 메서드의 경우, 매개 변수로 `int a, int...b`를 받는 메서드와 `int...a` 메서드를 구분하지 못한다는 뜻이다.</br></br>

# Overriding 오버라이딩
> </br>조상 클래스로부터 상속받은 메서드를 변경할 수 있다. </br></br>

오버라이딩을 활용하려면 `상속`의 개념을 알아야 하지만, 깊게 다루지는 않는다. Java에서는 한 클래스가 가진 멤버 변수, 메서드를 다른 클래스에게 물려줄 수 있다. 그래서 물려주는 클래스를 `부모 클래스`라고 하고, 물려받는 클래스를 `자식 클래스`라고 한다. 자식 클래스는 부모 클래스로부터 물려받은 멤버 변수, 메서드 이외에도 자신만의 속성을 가질 수 있다.
```
class Parent{
    String name = Patrick;
    String house;

    void enterHouse(){
        System.out.println("Parent Going Home");
    }
}

class Son extends Parents{
    String name = Dorie;

    void enterHouse(){
        System.out.println("Dorie Going Home");
        super.enterHouse();
        System.out.println("name : " + name);
        System.out.println("this.name : " + this.name);
        System.out.println("super.name : " + super.name);
    }
}
```
이 때 `Son` 클래스는 `Parents` 클래스의 `name`, `house`, `enterHouse()` 메서드를 사용할 수 있다. 예를 들면 아래와 같다.
```
class main{
    Son anny = new Son();
    anny.enterHouse();
}
```
```
Dorie Gong Home
Parent Going Home
name : Dorie
this.name : Dorie
super.name : Patrick

```
위의 예시에서, 자식 클래스에서 `this`는 자기 자신을, `super`는 부모 클래스의 속성을 불러올 때 사용되는 명령어라는 것을 알 수 있다.

오버라이딩의 아래와 같다.

1. 이름이 같아야 한다.
2. 매개변수가 같아야 한다.
3. 반환타입이 같아야 한다.

오버라이딩의 조건은 다음과 같다.

1. 접근 제어자를 조상 클래스의 메서드보다 좁은 범위로 설정할 수 없다.
2. 예외는 조상 클래스의 메서드보다 많이 선언할 수 없다.
3. 인스턴스 메서드를 static 메서드로 또는 그 반대로 변경할 수 없다.

2번 조건에서 오해가 생길 수 있는데, 많이 선언할 수 없다는 것은 개수와 종류를 의미한다. 만약 부모 클래스가 `IOException, SQLException` 예외를 가지고 있다면 자손 클래스가 `Exception` 예외를 갖진 못한다. `Exception`은 `IOException`이나 `SQLException`보다 범위가 넓기 때문이다.

오버라이딩을 오버로딩과 같은 페이지에 넣은 것은, 헷갈리기 쉽기 때문이다.</br>

<h3>1. 오버로딩 : 메서드를 새로 만드는 것</br>
2. 오버라이딩 : 기존에 있던 메서드를 변경하는 것</h3>