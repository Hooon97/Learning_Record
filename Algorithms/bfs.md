# Breadth First Search 너비 우선 탐색
**탐색**은 주어진 데이터에서 자신이 원하는 데이터를 찾아내는 행위를 말한다. 정렬 데이터인지, 비정렬 데이터인지에 따라 효율적인 탐색 기법(알고리즘)이 존재한다.</br>

너비 우선 탐색(BFS)는 분기를 파고들어 탐색하는 DFS와 달리, 시작 노드를 기준으로 시작 노드와 가까운 노드들을 우선적으로 탐색한다. 수면 위에 떨어진 물방울이 일으키는 파장을 떠올려보자. 이러한 특성으로, BFS를 이용한 탐색은 **최단 경로를 보장**한다.</br>

너비 우선 탐색의 시간 복잡도는 `O(V+E)`로 DFS와 동일하다. V와 E는 노드와 에지의 개수이다.</br>
단, `Queue`를 이용하여 구현할 수 있고, `Queue`는 **선입선출, FIFO**의 특징을 가지고 있다.</br>

백준 [DFS와 BFS](https://www.acmicpc.net/problem/1260) 문제를 통해 구현해보자.</br>
```
package own;

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class 복습 {
	static ArrayList<Integer>[] A;
	static boolean[] visit;
	static StringBuilder sb;
	public static void main(String[] args) throws Exception{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		sb = new StringBuilder();
		int N = Integer.valueOf(st.nextToken());
		int M = Integer.valueOf(st.nextToken());
		int V = Integer.valueOf(st.nextToken());
		A = new ArrayList[N+1];
		visit = new boolean[N+1];
		for(int i = 1; i<N+1; i++) {
			A[i] = new ArrayList<>();
		}
		
		for(int i = 0; i<M; i++) {
			st = new StringTokenizer(br.readLine());
			int start = Integer.valueOf(st.nextToken());
			int end = Integer.valueOf(st.nextToken());
			A[start].add(end);
			A[end].add(start);
		}
		
		for(int i = 1; i<N+1; i++) {
			Collections.sort(A[i]);
		}
		
		DFS(V);
		sb.append("\n");
		Arrays.fill(visit, false);
		BFS(V);
		
		System.out.print(sb.toString());
	}
	private static void DFS(int v) {
		if(visit[v]) return;
		visit[v] = true;
		sb.append(v+" ");
		for(int n : A[v]) {
			if(visit[n]) continue;
			DFS(n);
		}
	}
	private static void BFS(int v) {
		Queue<Integer> q = new LinkedList<>();
		q.add(v);
		visit[v] = true;
		sb.append(v+" ");
		
		while(!q.isEmpty()) {
			int cur = q.poll();
			for(int n : A[cur]) {
				if(visit[n]) continue;
				visit[n] = true;
				sb.append(n+" ");
				q.add(n);
			}
		}
	}
}
```
`DFS`는 재귀를 통해 구현하는데 반해, `BFS`는 `Queue`를 이용하여 구현하고 있다.</br>
`Queue`에는 시작 노드가 입력되고, 시작 노드를 기준으로 아직 방문하지 않은 노드들을 탐색한다. 방문하지 않았다면 해당 노드를 방문처리하고, `Queue`에 넣어둔다. Queue는 먼저 들어온 값들이 먼저 빠져나오는 FIFO, 선입선출의 성질이 있으므로 현재 노드와 가장 가까운 관계에 있는 노드들을 우선적으로 탐색하게 된다.