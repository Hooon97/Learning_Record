# 순열
집합 내의 원소들을 순서가 있는 상태로 나열한다. 이 때 중복 순열은 중복된 원소를 허용한다.
```
package own;

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.PriorityQueue;
import java.util.StringTokenizer;

public class 복습 {
	private static int n, m;
	private static int[] arr;
	private static boolean[] visit;
	public static void main(String[] args) throws Exception{
		n = 4; // 총 원소의 개수
		m = 2; // 뽑을 원소의 개수
		arr = new int[m];
		visit = new boolean[n+1];
		permutation(0);
        repeatedPermutation(0)
	}
	private static void permutation(int depth) {
		if(depth == m) {
			System.out.println(Arrays.toString(arr));
			return;
		}
		for(int i = 1; i<n+1; i++) {
			if(visit[i]) continue;
			visit[i] = true;
			arr[depth] = i;
			permutation(depth+1);
			visit[i] = false;
		}
	}
	
	private static void repeatedPermutation(int depth) {
		if(depth == m) {
			System.out.println(Arrays.toString(arr));
			return;
		}
		for(int i = 1; i<n+1; i++) {
			arr[depth] = i;
			repeatedPermutation(depth+1);
		}
	}
```
```
// 일반 순열 결과
[1, 2]
[1, 3]
[1, 4]
[2, 1]
[2, 3]
[2, 4]
[3, 1]
[3, 2]
[3, 4]
[4, 1]
[4, 2]
[4, 3]
```
```
//중복 순열 결과
[1, 1]
[1, 2]
[1, 3]
[1, 4]
[2, 1]
[2, 2]
[2, 3]
[2, 4]
[3, 1]
[3, 2]
[3, 3]
[3, 4]
[4, 1]
[4, 2]
[4, 3]
[4, 4]

```