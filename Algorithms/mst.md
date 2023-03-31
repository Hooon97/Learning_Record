# Minimum Spanning Tree 최소 신장 트리(MST)
최소 신장 트리는 주어진 그래프의 모든 노드들을 연결할 때, 가중치의 합이 최소인 트리를 의미한다. 에지 리스트로 그래프를 표현하고, `유니온 파인드` 알고리즘으로 사이클 생성을 방지할 수 있다.</br>
우선순위 큐로 가중치가 가장 작은 순서대로 나열하고, 그 순서대로 검사한다. 이 때 부모가 달라 사이클이 생성되지 않는다면 연결하고, 부모가 같아 사이클이 생성된다면 연결하지 않고 넘어간다.</br>
간선 중심, 즉 에지 중심의 알고리즘이기 때문에 주어진 에지들을 기준으로 검사하는게 특징이다.

</br>

백준 [최소 스패닝 트리](https://www.acmicpc.net/problem/1197) 문제를 예시로 들어보자.
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
	static PriorityQueue<Edge> q;
	public static void main(String[] args) throws Exception{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		q = new PriorityQueue<Edge>();
		StringTokenizer st = new StringTokenizer(br.readLine());
		int N = Integer.valueOf(st.nextToken()); // 노드의 수
		int M = Integer.valueOf(st.nextToken()); // 에지(간선)의 수
		parent = new int[N+1];
		for(int i = 1; i<N+1; i++)
			parent[i] = i;
		for(int i = 0; i<M; i++) {
			st = new StringTokenizer(br.readLine());
			int s = Integer.valueOf(st.nextToken());
			int e = Integer.valueOf(st.nextToken());
			int v = Integer.valueOf(st.nextToken());
			q.add(new Edge(s, e, v));
		}
		
		int useEdge = 0;
		int result = 0;
		while(useEdge < N-1) {
			Edge now = q.poll();
			if(find(now.s) != find(now.e)) {
				union(now.s,now.e);
				result += now.v;
				useEdge++;
			}
		}
		System.out.println(result);
	}
	static void union(int a, int b) {
		a = find(a);
		b = find(b);
		if(a != b) parent[b] = a;
	}
	static int find(int a) {
		if(a == parent[a]) {
			return a;
		}
		else {
			return parent[a] = find(parent[a]);
		}
	}
}
class Edge implements Comparable<Edge>{
	int s, e, v;
	Edge(int s, int e, int v){
		this.s = s;
		this.e = e;
		this.v = v;
	}
	@Override
	public int compareTo(Edge eEdge) {
		if(this.v > eEdge.v) return 1;
		else return -1;
	}
}


``` 