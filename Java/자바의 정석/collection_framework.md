# Collection Framework 컬레션 프레임워크

컬렉션 프레임워크는 **다수의 데이터(Collection)** 을 **규칙화된 방법(Framework)** 으로 다루기 위해 Java에서 객체지향적으로 설계한 자료 구조(Data Structure) 인터페이스다. </br>
크게 세 가지의 핵심 인터페이스가 있다.

|타입|구현 클래스|특징|
|----|----------|----|
|List|ArrayList, LinkedList, Stack, Queue, Vector ...| 순서가 있고, 중복을 허용|
|Set|HashSet, TreeSet ...|순서가 없고, 중복을 허용하지 않음|
|Map|키(Key)와 값(Value)을 한 쌍(Pair)로 자료를 저장하며, </br>순서가 없고 키(key)는 중복을 허용하지 않는다. 값(Value)은 중복을 허용한다.|HashMap, TreeMap, Hashtable, Properties...|

이 중에서 `Vector`, `Stack`, `HashTable`, `Properties`등의 자료구조는 컬렉션 프레임워크의 명명법을 따르지 않는다. 즉, 이름만으로 기능을 유추할 수 없다는게 특징인데, 컬렉션 프레임워크가 고안되기 이전에 존재하던 자료구조이기 때문이다.</br>
특히 `Vector`, `HashTable`은 기존에 설계된 클래스들과의 호환을 위해 남겨두었지만, 그보다는 `ArrayList`나 `HashMap` 등 새롭게 설계된 클래스 위주로 활용하자.</br>

## Collection, List, Set, Map 인터페이스

