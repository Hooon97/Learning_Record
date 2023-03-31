# Dijkstra 다익스트라
그래프에서 최단 거리를 구하는 알고리즘이다.</br>
`에지가 모두 양수`일 때 적용할 수 있고, 시간 복잡도는 `O(ElogV)`이다.</br>
주의할 점이 있는데, 출발 노드에서 도착 노드까지의 최단 거리가 아니다. 출발 노드와 그 외 노드 간의 최단 거리를 구하는 알고리즘이다. 만약 출발 노드의 번호가 1이고 노드 번호가 1,2,3,4,5가 있다면, 결과로 반환되는 최단 거리 배열의 값은 1번 노드에서 2,3,4,5번에 최단 거리로 도착할 수 있는 거리를 의미한다.</br>
구현 예시는 아래와 같다. 백준 문제를 예시로 들었다.</br></br>
[최단경로](https://www.acmicpc.net/problem/1753)
```
package own;

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;
import java.util.PriorityQueue;
import java.util.Scanner;
import java.util.StringTokenizer;

public class 복습 {
	public static int V,E,K;
	public static int distance[];
	public static boolean[] visited;
	public static ArrayList<Edge>[] list;
	public static PriorityQueue<Edge> q = new PriorityQueue<>();
	public static void main(String[] args) throws Exception{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringBuilder sb = new StringBuilder();
		StringTokenizer st = new StringTokenizer(br.readLine());
		V = Integer.valueOf(st.nextToken()); // 정점의 개수
		E = Integer.valueOf(st.nextToken()); // 간선의 개수
		K = Integer.valueOf(br.readLine()); // 시작 정점의 번호
		
		distance = new int[V+1];
		Arrays.fill(distance, Integer.MAX_VALUE);
		distance[K] = 0;
		
		visited = new boolean[V+1];
		
		list = new ArrayList[V+1];
		for(int i = 1; i<V+1; i++)
			list[i] = new ArrayList<Edge>();
		
		//방향 그래프에 정보 입력
		for(int i = 0; i<E; i++) {
			st = new StringTokenizer(br.readLine());
			int u = Integer.valueOf(st.nextToken());
			int v = Integer.valueOf(st.nextToken());
			int w = Integer.valueOf(st.nextToken());
			list[u].add(new Edge(v, w));
		}
		
		//우선순위 큐를 사용한 다익스트라
		q.add(new Edge(K, 0));
		while(!q.isEmpty()) {
			Edge cur = q.poll();
			int c_v = cur.vertex;
			int c_w = cur.value;
			if(visited[c_v]) continue;
			visited[c_v] = true;
			
			//해당 엣지와 연결된 엣지 탐색
			for(Edge e : list[c_v]) {
				int next_vertex = e.vertex;
				int next_value = e.value;
				if(distance[next_vertex] > distance[c_v]+next_value) {
					distance[next_vertex] = distance[c_v] + next_value;
					q.add(new Edge(next_vertex, distance[next_vertex]));
				}
			}
		}
		
		for(int i = 1; i< V+1; i++) {
			if(visited[i]) sb.append(distance[i]+"\n");
			else sb.append("INF\n");
		}
		System.out.print(sb.toString());
	}
}
class Edge implements Comparable<Edge>{
	int vertex, value;
	Edge(int vertex, int value){
		this.vertex = vertex;
		this.value = value;
	}
	
	@Override
	public int compareTo(Edge e) {
		if(this.value > e.value) return 1;
		else return -1;
	}
	
}
```
앞서 그래프의 [3가지 표현 방식](../Algorithms/graph_types.md) 중 인접 리스트로 그래프를 표현했다. 로직의 알고리즘은 꽤 단순한데, 4번이 핵심이다.
1. 에지(Edge, 이하 노드)K번 노드에서 다른 노드로 갈 수 있는 최단 거리 배열을 선언한다. 
2. 시작 노드인 K번 노드는 0이다. 최단 거리 배열의 초기 상태는 K번 노드를 제외하곤 무한히 큰 수이다.
3. K번 노드를 시작으로, K번 노드에서 갈 수 있는 다른 노드들을 탐색하며 값을 비교한다.
4. 값을 비교하는 로직은, "K번 노드에서 다음 노드까지 오는데 최단거리는 ~~이야. 이 때, 최단 거리 배열에서 현재 노드 번호의 거리와 다음 노드까지 갈 때 걸리는 거리를 비교"한다.
5. 최단 거리 배열의 값이 더 크면 값을 교체한다.
6. 이 때 한 번 방문한 노드는 재방문 하지 않도록 `boolean[] visit`을 통해 방문처리를 해야한다.
7. 일종의 BFS라고 보면 될 듯 하다.

우선순위 큐(Priorirt Queue)를 적용하여 구현한 다익스트라 알고리즘은 개선된 형태의 구현 방식이다. 우선순위 큐를 통해 해당 노드에서 갈 수 있는 다음 노드들의 거리 중 최솟값을 자동 정렬해놓지 않으면, 최솟값 노드를 찾는 로직을 한번 더 수행해줘야 한다. 이 경우 시간 복잡도는 최악의 경우 `O(V^2)`가 될 수 있다.</br>

그래도 다익스트라 알고리즘이 정말 노드간 최단 거리를 구하는 게 맞는지 의심이 들 수 있다. 이게 정상인게, 다익스트라 알고리즘은 그리디 알고리즘을 기반에 두고 있기 때문이다. 나도 종종 의심이 들 때가 있다.</br>
링크를 통해 다익스트라에 대한 자세한 설명을 읽을 수 있다.</br>
[[Java]다익스트라 알고리즘(Dijkstra Algorithm)](https://sskl660.tistory.com/59)
