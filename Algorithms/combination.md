# Combination
집합 내의 원소를 순서를 고려하지 않고 뽑는 경우의 수를 의미한다. 중복 조합은 중복을 허용하는 조합이다.
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

		combination(0,1);
	}	
	private static void combination(int depth, int start) {
		if(depth == m) {
			System.out.println(Arrays.toString(arr));
			return;
		}
		
		for(int i = start; i<n+1; i++) {
			arr[depth] = i;
			combination(depth+1, i+1);
		}
	}
	
	private static void repeatedCombination(int depth, int start) {
		if(depth == m) {
			System.out.println(Arrays.toString(arr));
			return;
		}
		
		for(int i = start; i<n+1; i++) {
			arr[depth] = i;
			combination(depth+1, i);
		}
	}
}
```
```
// 일반 조합 결과
[1, 2]
[1, 3]
[1, 4]
[2, 3]
[2, 4]
[3, 4]

```
```
// 중복 조합
[1, 1]
[1, 2]
[1, 3]
[1, 4]
[2, 2]
[2, 3]
[2, 4]
[3, 3]
[3, 4]
[4, 4]
```
