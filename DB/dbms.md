# DBMS
`DBMS`는 DataBase Management System의 약자로 데이터베이스 관리 시스템, 즉 **자료 관리 소프트웨어**다. 친숙한 예시로는 MySQL, Oracle, MongoDB 등이 있다. `데이터베이스(Database)`는 **데이터의 집합**을 의미한다. 데이터 생성, 삭제, 삽입, 수정, 조회 등의 여러 기능을 제공한다. 이런 관점에선 엑셀도 DBMS의 일종이라고 볼 수 있는데, DBMS는 주로 대규모 데이터베이스를 대상으로 하기 때문에 엑셀은 DBMS라고 하지 않는다.</br>

## 초기 DBMS
최초의 DBMS, 즉 데이터를 관리하는 방식은 종이와 펜이었다. 컴퓨터가 등장하고 나서 `파일(file)` 형태로 자료를 기록하였다. 이 수준에서 엑셀이 주로 사용되었다. 하지만 엑셀은 동시 작업이 불가능하고, 여러 작업자간에 작업 내역 공유가 어렵다. 소규모 데이터를 처리하는데는 아주 효율적이지만, 대규모 데이터에 대해에서는 좀 더 보안된 방식이 필요했다.</br>

이 후 대량의 데이터를 효율적으로 관리하고 운용하기 위해 등장한 것이 `DBMS`이다. `DBMS`에 `DB`를 구축하고 관리, 활용할 수 있다. 이 때 사용되는 언어가 `SQL`로, Structured Query Langauge의 준말이다.

## DBMS의 종류
### Hierarchical DBMS 계층형 DBMS
`트리(Tree)` 형태의 DBMS다. 회사 조직도를 생각하면 이해가 쉽다. 이 형태의 DBMS는 한 번 DB 구성이 완료되면 수정이 까다롭고, 계층을 따라 데이터를 탐색하는 과정이 번거롭다는 단점이 있다. 비효율적이라서 이제는 쓰이지 않는다.</br>

### Network DBMS 망형 DBMS
계층형 DBMS의 단점을 보완하여, 수직적으로 연결되어있던 데이터 뭉치들의 연결 관계가 더욱 확장된 형태를 띈다. 예를들어 계층형 DBMS에서 `사장`은 `이사`와 연결되어있고, `이사`는 `부서별 팀`에 연결되어있었다. 이 때 부서는 독립적으로 존재하여 서로 탐색할 수 없었다. 하지만 망형 DBMS에서는 부서끼리, 서로 다른 부서의 이사와 팀끼리 연결되어있다.</br>
개발자가 DB구조를 완전히 숙지하고 나서야 활용이 가능하다는 단점 때문에 더이상 쓰이지 않는다.</br>

### Relational DBMS 관계형 DBMS
관계형 DBMS, `RDBMS(Relational DataBase Management System)`이라고 한다. MySQL, Oracle이 대표적인 RDBMS 소프트웨어이다. 데이터 뭉치의 최소 단위는 `테이블(Table)`이라 하며, 각 테이블은 `행(Row)`과 `열(Column)`으로 이루어져있다.</br>
최근까지 대부분의 데이터베이스가 관계형 DBMS일 정도로 대중적인 데이터 관리 시스템이다. RDBMS에서는 SQL을 활용하여 데이터를 조작할 수 있다. 하지만 RDBMS 소프트웨어는 회사별로 각각 존재한다. 모든 제품마다 다른 문법을 표방할 순 없으니, 국제표준화기구에서 지정한 `표준 SQL`을 공통으로 삼되, 각 제품의 특성에 맞게 확장하여 사용한다. 즉, 표준 SQL을 익히면 다양한 DBMS의 공통적인 부분을 학습하는 것이다.

### Non-Relational DMBS 비관계형 DBMS
여러 종류의 NoSQL이 있지만, 모든 NoSQL의 공통점은 RDBMS를 사용하지 않는다는 점이다. 비관계형 데이터 베이스를 왜 굳이 `NoSQL`, 비구조화된 DBMS라고 할까?</br>
RDBMS를 SQL 이라고도 부르기 때문이다. `SQL`은 애초에 RDBMS 전용 언어이다. `NoSQL`이라고 하면 관계형 데이버테이스가 아닌 것, 즉 비관계형 데이터베이스를 의미한다.</br>
`NoSQL`은 데이터 모델에 따라 유형이 다양하다. `문서(Document)`, `키-값(Key-Value)`, `와이드 컬럼(Wide-Column)`, `그래프(Graph)` 등등.. 많다. NoSQL DBMS에서는 `쿼리(Query)`를 통해 데이터를 조회할 수 있다. </br>
RDBMS랑 다른 점은, RDBMS는 테이블의 스키마를 통해 데이터를 조회, 즉 테이블의 형식과 관계를 고려하여 데이터를 요청하지만, `NoSQL`의 `쿼링(Querying)`은 데이터 그룹 자체를 조회하는데 초점을 둔다.</br>
데이터끼리의 스키마도 없고 관계성도 없으므로, 다음과 같은 장점이 있다.

1. 수직적, 수평적 확장이 가능하다. -> 데이터 유연성이 좋다.
2. 대용량 데이터 처리에 용이하다.
3. 검색에 유리하고, 응답 속도와 처리 효율 성능이 뛰어나다.

단점도 있다.

1. 쿼리를 처리할 때 `데이터 파싱 - 연산` 과정을 거치기 때문에 문서의 크기가 클 때는 성능이 저하될 수 있다.

상황에 맞는 DBMS를 사용하는 것이 필요하다.