# Depth First Search 깊이 우선 탐색
**탐색**은 주어진 데이터에서 자신이 원하는 데이터를 찾아내는 행위를 말한다. 정렬 데이터인지, 비정렬 데이터인지에 따라 효율적인 탐색 기법(알고리즘)이 존재한다.</br>

깊이 우선 탐색(DFS)는 그래프의 시작 노드에서 출발하여 최대 깊이의 분기까지 탐색한 후, 다른 분기로 이동하여 탐색을 진행한다. **완전 탐색 기법**이다.</br>

시간 복잡도는 `O(V+E)`이고, V와 E는 노드와 에지의 개수이다.</br>

`재귀 함수(Recursion)` 혹은 `스택(Stack)`을 통해 구현할 수 있다.</br>

백준 [연결 요소의 개수](https://www.acmicpc.net/problem/11724)
```
package own;

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.StringTokenizer;

public class 복습 {
	static ArrayList<Integer>[] A;
	static boolean[] visit;
	public static void main(String[] args) throws Exception{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		int N = Integer.valueOf(st.nextToken());
		int M = Integer.valueOf(st.nextToken());
		int count = 0;
		visit = new boolean[N+1];
		A = new ArrayList[N+1];
		for(int i = 1; i<N+1; i++) {
			A[i] = new ArrayList<Integer>();
		}
		
		for(int i = 0; i<M; i++) {
			st = new StringTokenizer(br.readLine());
			int start = Integer.valueOf(st.nextToken());
			int end = Integer.valueOf(st.nextToken());
			A[start].add(end);
			A[end].add(start);
		}
		
		for(int i = 1; i<N+1; i++) {
			if(visit[i]) continue;
			count++;
			DFS(i);
		}
		
		System.out.print(count);
	}
	private static void DFS(int node) {
		if(visit[node]) return;
		visit[node] = true;
		for(int n : A[node]) {
			if(visit[n]) continue;
			DFS(n);
		}
	}
}
```

일반적으로 재귀 함수를 호출하여 구현하는 것이 더 간단하고 코드를 이해하기 좋다. 이미 탐색한 노드를 저장하는 `visit` 배열이 선언되고, 인접 리스트로 선언하였다.