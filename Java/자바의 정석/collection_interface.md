# Collection Interfaces
## List 인터페이스
### ArrayList
1. List interface를 구현하는 클래스이고 기존의 `Vector` 클래스를 개선한 것이다.
2. `Object` 배열을 이용해 **순차적으로** 데이터를 저장한다.
3. 데이터를 **읽거나** **저장**하는데 효율이 좋다.
4. 비순차적 **데이터의 추가**, **삭제**에 시간이 많이 걸린다.
5. 배열에 저장할 공간이 없으면 기존 배열보다 두 배 큰 배열을 새로 생성하고, 기존 배열을 새 배열에 복사한다.</br>이 특성 때문에 효율이 떨어지기도 한다.

### LinkedList
1. List interface를 구현하는 클래스이고, `ArrayList`가 가진 4번 결점을 보완한다.
2. **데이터를 불연속적**으로 서로 **연결**한다.
3. 따라서 데이터를 읽는 효율은 낮다. 모든 요소를 살펴야 하므로, n개의 데이터 있을 때 시간 복잡도는 O(n)이다.
4. 그러나 순차적, 비순차적 **데이터의 삭제, 추가**가 간단하다.
5. Linked List - Double Linked List - Double Circular Linked List는 순차적으로 발전되는 형태를 띈다. `LinkedList` 클래스는 Double Circular Linked List로 구현되어 있다.

### Stack
1. `Stack`은 클래스를 제공한다.
2. 따라서 `Stack<String> test = new Stack<String>()`의 형태로 선언 가능하다.
3. LIFO 구조로, 가장 나중에 들어온 데이터가 가장 먼저 반환된다.
4. 구현한다면, 순차적으로 데이터를 꺼내는 `ArrayList`같은 배열 기반의 클래스가 적절하다. 배열의 끝 데이터를 반환하고, 삭제하기 때문이다.

### Queue
1. `Queue`는 인터페이스고, 이를 구현하는 여러 클래스들이 제공된다.
2. 그 중 일부가 `PriorityQueue`, `LinkedList`이다.</br>`Queue pq = new PrioritiQueue<>()`</br>`Queue<Integer> q = new LinkedList<br>()`</br>와 같이 사용할 수 있다.
3. **FIFO** 구조로, 먼저 들어온 데이터가 먼저 출력된다.
4. 구현한다면, 앞 단의 데이터를 출력하고 삭제하므로 `LinkedList`가 적절하다.

### Dequeue
1. `Queue` 인터페이스를 구현하는 클래스의 일종이다.
2. `Stack`나 `Queue`처럼 사용할 수 있는, 데이터를 순차적으로 저장하여 앞 단과 뒷 단에서 꺼낼 수 있는 자료 구조이다.

## Set 인터페이스
### HashSet
1. Set 인터페이스를 구현한 클래스로, 중복을 허용하지 않는다.
2. 저장 순서가 유지되지 않는다.

### LinkedHashSet
1. Set 인터페이스를 구현한 클래스로, 중복을 허용하지 않지만 저장 순서가 유지된다.
2. 사용 예시는 아래와 같다. `List`로 변환도 가능하다.

```
Set set = new HashSet();
Set linkedSet = new LinkedHashSet();

for(int i = 0; i<50; i++){
    set.add( (int)Math.random()*50+1 + "");
    linkedSet( (int)Math.random()*50+1 + "" );
}

// set -> list
List setList = new LinkedList(set);
List linkedSetList = new LinkedList(linkedSet);

Iterator setIt = new set.Iterator()
Iterator linkedIt = new linkedSet.Iterator()

for(int i = 0; i<50; i++){
    System.out.print(Integer.valueOf((String)setIt.next())+" ");
    System.out.println(Integer.valueOf((String)linkedIt.next()));
}
```
`Iterator`을 `String` 형변환 해주는 이유는, `Object`타입이기 때문이다.

### TreeSet
1. 이진 검색 트리(binary Search Tree) 형태로 데이터를 저장한다. 레드-블랙 트리(Red-Black Tree)로 구현되어 있다. 따라서 **정렬**, **검색**, **범위 검색**을 빠르게 수행한다.
2. 중복을 허용하지 않으며, 저장 순서를 유지지 않는다.
3. 정렬을 커스터마이징 하고 싶다면, 객체 내에 `Comparable`을 구현하거나 `TreeSet`에 `Comparator`를 제공해야한다.

|메서드 이름|특징|
|----------|---|
|`subSet(Object a, Object b)`|a에서 b 사이의 값들을 반환한다. a는 포함, b는 비포함|
|`headSet(Object toElement)`|지정된 객체보다 작은 값의 객체들을 반환한다.|
|`headSet(Object toElement, boolena inclusive)`|inclusive가 true이면 이하 값을, false면 미만 값들을 반환|
|`tailSet(Object fromElement)`|지정된 객체보다 큰 값의 객체들을 반환한다.|
|`higher(Object o)`|지정된 객체보다 큰 값 중 가장 가까운 객체를 반환|
|`lower(Object o)`|지정된 객체보다 작은 값 중 가장 가까운 객체를 반환|
|`toArray()`|객체를 객체 배열로 반환한다.|

## Map 인터페이스
### HashMap
1. `Map`을 구현했으며 키(Key)와 값(Value)를 하나의 데이터(Entry)로 저장한다.
2. 해싱(Hashing)을 통한 데이터 저장으로 **데이터 검색**에 강점을 보인다.
3. 키(Key)는 중복을 허용하지 않고, 값(Value)는 중복을 허용한다.

