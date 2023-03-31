# Union-Find 유니온 파인드
여러 노드의 연관 관계를 집합을 통해 표현하는 알고리즘이다. 특정 두 노드를 하나로 묶는 연산은 `union`이라 하고, 특정 노드의 부모 노드, 즉 해당 노드가 포함되어있는 집합을 찾는 연산을 `find`라 한다.</br>
코드의 구현 자체는 재귀를 통해 표현되어 무척 간단하다.</br>
백준 [집합의 표현](https://www.acmicpc.net/problem/1717) 문제를 통해 살펴보자.
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
	static int[] parent;
	public static void main(String[] args) throws Exception{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringBuilder sb = new StringBuilder();
		StringTokenizer st = new StringTokenizer(br.readLine());
		int N = Integer.valueOf(st.nextToken());
		int M = Integer.valueOf(st.nextToken());
		parent = new int[N+1];
		
		for(int i = 0; i<N+1; i++) parent[i] = i;
		for(int i = 0; i<M; i++) {
			st = new StringTokenizer(br.readLine());
			if(Integer.valueOf(st.nextToken()) == 0) {
				union(Integer.valueOf(st.nextToken()), Integer.valueOf(st.nextToken()));
			}
			else {
				if(find(Integer.valueOf(st.nextToken())) == find(Integer.valueOf(st.nextToken()))) {
					sb.append("yes\n");
				}
				else sb.append("no\n");
			}
		}
		System.out.print(sb.toString());
	}
	static void union(int a, int b) {
		a = find(a);
		b = find(b);
		if(a != b) parent[b] = a;
	}
	static int find(int a) {
		if(a == parent[a]) return a;
		else {
			return parent[a] = find(parent[a]);
		}
	}
}
```
`union` 연산과 `find` 연산의 동작 과정이 어떻게 이루어져있는지만 이해하면 된다. 유니온-파인드 알고리즘은 이 후 플로이드-워셜 알고리즘에서 사이클을 판단하기 위해 사용되기도 한다.