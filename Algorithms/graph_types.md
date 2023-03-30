# 그래프의 표현
## 인접 행렬
2차원 배열 구조를 자료 구조로 활용하여 그래프를 표현한다.</br>
노드 중심으로 그래프를 표현하며, 그 예시는 다음과 같다.</br>
1. 인접 행렬을 이용한 유향 무가중 그래프

노드가 5개인데 인접 행렬의 크기는 6x6으로 선언했다. 인덱스는 0부터 시작하지만 노드는 1부터 시작하므로, 인덱스와 노드를 통일시켜주기 위함이다.
```
입력 : 
1 2
2 4
1 3
2 5
4 5
3 4
```
```
public class 복습 {
	public static void main(String[] args) throws Exception{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int[][] map = new int[6][6];
		
		//입력 받기 - 유향 그래프
		for(int i = 0; i<5; i++) {
			StringTokenizer s = new StringTokenizer(br.readLine());
			int st = Integer.valueOf(s.nextToken());
			int ed = Integer.valueOf(s.nextToken());
			map[st][ed] = 1;
		}
		
		System.out.println();
		for(int i = 0; i<5; i++) {
			System.out.println(Arrays.toString(map[i]));
		}
	}
}
```
결과는 아래와 같다.
```
[0, 0, 0, 0, 0, 0]
[0, 0, 1, 1, 0, 0]
[0, 0, 0, 0, 1, 1]
[0, 0, 0, 0, 0, 0]
[0, 0, 0, 0, 0, 1]
```

2. 인접 행렬을 이용한 무향 무가중 그래프

달라진 점은 크게 없다. 무방향이므로 시작점과 도착점이 구분되지 않고, 따라서 인접 행렬에 입력해주는 과정이 한 번 더 있어야 한다.
```
public class 복습 {
	public static void main(String[] args) throws Exception{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int[][] map = new int[6][6];
		
		//입력 받기 - 유향 그래프
		for(int i = 0; i<5; i++) {
			StringTokenizer s = new StringTokenizer(br.readLine());
			int st = Integer.valueOf(s.nextToken());
			int ed = Integer.valueOf(s.nextToken());
			map[st][ed] = 1;
			map[ed][st] = 1;
		}
		
		System.out.println();
		for(int i = 0; i<5; i++) {
			System.out.println(Arrays.toString(map[i]));
		}
	}
}
```
```
[0, 0, 0, 0, 0, 0]
[0, 0, 1, 1, 0, 0]
[0, 1, 0, 0, 1, 1]
[0, 1, 0, 0, 0, 0]
[0, 0, 1, 0, 0, 1]
```
가중치가 있는 경우면 1대신 가중치를 입력하면 된다.
</br>

인접 행렬은 표현이 간단하고 이해가 직관적이지만, 탐색을 할 때 필요없는 인덱스 (값이 0인 부분)도 탐색해야 하므로 효율이 떨어진다. 꼭 사용해야하는 순간도 있다.

## 인접 리스트
`ArrayList`를 활용해 그래프를 표현한다. 그래프의 구현이 복잡한 편이지만 에지 탐색 시간이 뛰어나고, 공간 복잡도도 낮은 편이다. 따라서 코딩 테스트에 자주 쓰인다. 예시는 아래와 같다.

1. 인접 리스트를 이용한 무향 가중 그래프

보통 가중치가 입력될 때 인접 리스트로 표현하려면, `Node` 자료 구조를 스스로 정의하고, 이를 통해 표현할 수 있다. 가중치가 없는 경우는 `ArrayList<Integer>`로도 충분하다.
```
입력 : 
1 2 8
2 4 4
1 3 3
2 5 15
4 5 2
3 4 13
```
```
public class 복습 {
	public static void main(String[] args) throws Exception{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		ArrayList<Node>[] map = new ArrayList[6];
		for(int i = 1; i<6; i++) {
			map[i] = new ArrayList<Node>();
		}
		
		//입력 받기 - 유향 그래프
		for(int i = 0; i<5; i++) {
			StringTokenizer s = new StringTokenizer(br.readLine());
			int st = Integer.valueOf(s.nextToken());
			int ed = Integer.valueOf(s.nextToken());
			int weight = Integer.valueOf(s.nextToken());
			map[st].add(new Node(ed, weight));
			map[ed].add(new Node(st, weight));
		}
		
		System.out.println();
		for(int i = 1; i<6; i++) {
			for(Node n : map[i]) {
				System.out.println("node : "+i+" "+" next : "+n.node+" "+n.weight);
			}
		}
	}
	static class Node{
		int node;
		int weight;
		Node(int node, int weight){
			this.node = node;
			this.weight = weight;
		}
	}
}
```
결과는 아래와 같다.
```
node : 1  next : 2 8
node : 1  next : 3 3
node : 2  next : 1 8
node : 2  next : 4 4
node : 2  next : 5 15
node : 3  next : 1 3
node : 4  next : 2 4
node : 4  next : 5 2
node : 5  next : 2 15
node : 5  next : 4 2
```
방향이 있는 그래프의 경우, 인접 행렬에서 했던건과 동일하게 한 줄의 코드만 삭제해주면 된다.</br>
`map[ed].add(new Node(st, weight));` 삭제하기.


## 에지 리스트
노드가 아닌 에지 중심의 표현 방식이다. 배열에 출발 노드, 도착 노드, 가중치를 입력하여 표현한다. 인접 행렬처럼 표현할수도, 인접 리스트처럼 표현할수도 있다. 인접 리스트로 표현하는 방식은 위와 비슷하므로 생략한다.</br>인접 리스트 입력 값을 인접 행렬의 방식으로 에지 리스트로 표현해보자. 조건은 가중치가 있는 유향 그래프이다.
```
입력 : 
1 2 8
2 4 4
1 3 3
2 5 15
4 5 2
3 4 13
```
```
public static void main(String[] args) throws Exception{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int[][] map = new int[3][6];
		
		for(int i = 0; i<6; i++) {
			StringTokenizer s = new StringTokenizer(br.readLine());
			int st = Integer.valueOf(s.nextToken());
			int ed = Integer.valueOf(s.nextToken());
			int weight = Integer.valueOf(s.nextToken());
			map[0][i] = st;
			map[1][i] = ed;
			map[2][i] = weight;
		}
		
		System.out.println();
		for(int i = 0; i<map[0].length; i++) {
			for(int j = 0; j<map.length; j++) {
				System.out.print(map[j][i]+" ");
			}
			System.out.println();
		}
	}
```
```
1 2 8
2 4 4
1 3 3
2 5 15
4 5 2
3 4 13
```
입력 값과 동일하게 출력된다. 근데 당연한게 입력값이 시작 노드, 도착 노드, 가중치로 입력되어, 에지 리스트 형식으로 입력되었기 때문이다.