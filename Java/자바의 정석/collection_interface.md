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


## Map 인터페이스


