# Floyd-Warshall 플로이드-워셜
그래프에서 최단 거리를 구하는 알고리즘으로, 모든 노드 간에 최단 경로를 탐색한다. 단, 음수 가중치가 있어도 수행할 수 있고 동적 계획법(DP)적 원리가 적용되어 있다. 거의 만능이 아닐까 싶은데 시간 복잡도가 `O(V^3)`이다. V는 노드 수이다. 상당히 느린 편. 노드의 개수 범위가 충분히 작다고 판단될 때 적용할 수 있다.</br>
S노드에서 E노드까지의 최단 거리를 구해주는다는 점에서 다익스트라와 비슷하고, 음수 가중치에서도 적용될 수 있다는 점에서 벨만-포드 알고리즘과 같다. 하지만 벨만-포드 알고리즘은 주로 음수 사이클을 찾는데 사용된다는 점이 다르다.</br>
핵심 원리는 **A노드에서 B노드까지 최단 경로에 C노드가 존재한다면, A->C 노드는 최단 경로, C->B 경로도 최단 경로라는 것이다.** 따라서 다음과 같은 도화식이 도출될 수 있다.</br>
`D[S][E] = Math.min(D[S][E], D[S][C]+D[C][E])`</br>
백준 [플로이드 문제](https://www.acmicpc.net/problem/11404)로 예시를 들어보겠다.

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
	static int N, M;
	static int[][] distance;
	public static void main(String[] args) throws Exception{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringBuilder sb = new StringBuilder();
		N = Integer.valueOf(br.readLine().trim()); // 도시의 개수
		M = Integer.valueOf(br.readLine().trim()); // 버스 노선의 개수
		distance = new int[N+1][N+1];
		for(int i = 1; i<N+1; i++) {
			for(int j = 1; j<N+1; j++) {
				if(i == j) {
					distance[i][j] = 0;
				}
				else {
					distance[i][j] = 10000001;
				}
			}
		}
		
		for(int i = 0; i<M; i++) {
			StringTokenizer st = new StringTokenizer(br.readLine());
			int s = Integer.valueOf(st.nextToken());
			int e = Integer.valueOf(st.nextToken());
			int v = Integer.valueOf(st.nextToken());
			if(distance[s][e] > v) {
				distance[s][e] = v;
			}
		}
		
		//플로이드 워셜 알고리즘
		for(int k = 1; k<N+1; k++) {
			for(int i = 1; i<N+1; i++) {
				for(int j = 1; j<N+1; j++) {
					if(distance[i][j] > distance[i][k] + distance[k][j]) {
						distance[i][j] = distance[i][k] + distance[k][j];
					}
				}
			}
		}
		
		for(int i = 1; i<N+1; i++) {
			for(int j = 1; j<N+1; j++) {
				if(distance[i][j] == 10000001)
					sb.append("0 ");
				else
					sb.append(distance[i][j]+" ");
			}
			sb.append("\n");
		}
		System.out.print(sb.toString());
	}
}
```
구현 자체는 어렵지 않다.
