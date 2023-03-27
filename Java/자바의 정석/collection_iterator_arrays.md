# 데이터 접근 인터페이스
컬렉션 프레임워크는 컬렉션에 저장된 데이터 요소들을 읽어들이는 방법을 표준화시켰다.

## Iterator Interface
`Iterator()`는 `Collection Interface`에 정의된 메서드이므로 `List Interface`나 `Set Interface`에도 포함되어 있다. 주로 반복문에 사용될 요량으로 활용된다. 사용 예시는 아래와 같다.
```
ArrayList a = new ArrayList();
Iterator i = c.iterator();

while(i.hasNext()){
    System.out.println(i.next());
}
```
`iterator()` 메서드는 `Iterator`인스턴스를 반환하고, 이 인스턴스는 `hasNext()`, `next()`, `remove()` 메서드를 제공한다.

## ListIterator
`Iterator`에 양방향 조회 기능을 추가하였다. 이름에서 알 수 있듯이 `List`와 연관이 깊다. `List` 인터페이스를 구현한 클래스인 경우에만 사용 가능하다. 사용 예시는 아래와 같다.</br>
```
ArrayList list = new ArrayList();
list.add(1);
list.add(2);
list.add(3);
list.add(4);

ListIterator it = list.listIterator();

while(it.hasNext()){
    System.out.println(it.next()); //순방향 조회
}

while(it.hasPrevious()){
    System.out.println(it.previous()); //역방향 조회
}
```

## Enumeration
`Iterator`의 구버전이다. 이전 버전으로 작성된 코드와의 호환을 위해 남겨두었다.

</br>

# 기본 제공 메서드
## Arrays
`Arrays` 클래스는 배열을 다루는데 유용한 메서드들이 정의되어 있다. 기본형 배열, 참조형 배열 모두 구현되어 있다.
|이름|용도|
|----|----|
|`copyOf()`|배열 전체 복사|
|`copyOfRange()`|배열 일부 복사|
|`fill()`|배열의 모든 요소를 지정된 값으로 채운다.|
|`setAll()`|배열을 채우는데 사용될 **함수**를 매개변수로 받는다.|
|`sort()`|배열을 정렬한다.|
|`binarySearch()`|정렬된 배열을 이진탐색하여 위치를 반환한다.|
|`equals()`|두 배열을 요소별로 비교하여 `boolean`을 반환한다.|
|`deepEquals()`|다차원 배열을 비교한다.|
|`toString()`|일차원 배열을 문자로 반환한다.|
|`deepToString()`|다차원 배열을 문자로 반환한다.|
|`asList(Obejct...a)`|배열을 `List`에 담아 반환한다.|
|`parallelXXX()`|`parallel`로 시작하는 메서드, 멀티 쓰레드 작업을 지원한다.|
|`spliterator()`|하나의 작업을 여러 작업으로 나누는 `Spliterator`를 반환, 멀티 스레드를 지원한다.|
|`stream()`|컬렉션을 스트림으로 반환한다.|

많기는 한데 취준생의 입장에선, 코딩 테스트를 칠 때 유용할 메서드들이 몇 있다. 알아두면 시간을 많이 아낄 수 있을 것 같다.

## Comparator, Comparable
`Comparaotr`, `Comparable` 둘 다 인터페이스로, `Arrays.sort()`에서 정렬 메서드를 지원한다. 기본적으로는 오름차순을 지원하나, 참조 배열의 정렬을 원하거나 특별한 규칙에 의한 정렬을 원한다면 오버라이딩을 통해 커스터마이징이 가능하다.
```
// java.util 패키지 소속
pulbic interface Comparator {
    int compare(Object o1, Object o2);
    boolean equals(Object obj);
}

// java.lang 패키지 소속
public interace Comparable {
    public int compareTo(Object o);
}
```
위의 코드에서 볼 수 있듯이, `compare`과 `compareTo` 메서드의 반환 타입은 정수형이다. `compareTo()`는 비교하는 두 수가 같으면 0, 비교 값보다 작으면 음수, 크면 양수를 반환한다. `compare()`도 마찬가지다.</br>

역순 정렬을 원한다고 해보자.
```
public static void main(String[] args){
    
    String[] str = {"cat", "Dog", "lion", "tiger"};

    Arrays.sort(str); // Dog, cat, lion, tiger
    Arrays.sort(str, String.CASE_INSENSITIVE_ORDER); // cat, Dog, lion, tiger
    Arrays.sort(str, new Descending());
}

class Descending implements Comparator{
    public int compare(Object o1, Object o2){
        if(o1 instanceof Comparable && o2 instanceof Comparable){
            Comparable c1 = (Comparable)o1;
            Comparable c2 = (Comparable)o2;
            return c1.compareTo(c2) * -1;
        }
    }
    return -1;
}
```
핵심은 `Comparator` 인터페이스의 `compare(Object o1, o2)` 메서드를 `Arrays.sort()` 메서드에 전달해주는 것이다. 또한, `compare(Object o1, Object o2)` 메서드는 리턴값이 `o1-o2`의 값이 음수면 앞자리로, 양수면 뒷자리로 배치한다.

## Collections
1. 멀티 스레드 환경에서 데이터 일관성을 위한 객체 동기화 메서드</br> `List syncList = Collections.synchronizedList(new ArrayList(...))`
2. 데이터 보호를 위한 읽기 전용 메서드</br> `List readOnlyList = unmodifiedList()`
3. 하나의 객체만 저장하는 싱글톤 컬렉션</br> `static List sigletonList(Object o)`

</br>