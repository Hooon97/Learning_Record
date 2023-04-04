# Binary Search 이진 탐색
이진 탐색(Binary Search)는 **데이터가 정렬된 상태**에서 적용 가능한 탐색 알고리즘이다. 데이터의 중앙 값과 탐색 값을 비교하며 탐색 데이터의 영역을 절반씩 줄여가는 것이 특징이다.</br>
시간 복잡도는 `O(logN)`으로 낮은 편이며, 구현과 원리가 간단하여 유용하게 사용된다.</br>

탐색의 과정은 아래와 같다.

1. 정렬된 데이터 셋의 중앙값을 선택한다.
2. 중앙값과 탐색값을 비교하여, 중앙값이 더 크면 왼쪽 데이터 셋을 선택한다.
3. 중앙값이 더 작으면 중앙값 기준 오른쪽 데이터 셋을 선택한다.
4. 반복하면서 탐색값을 찾으면 반복을 종료한다.

</br>

백준 [기타 레슨](https://www.acmicpc.net/problem/2343)을 구현하며 실습해보자.
```
package own;

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class 복습 {
	public static void main(String[] args) throws Exception{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer stringToken = new StringTokenizer(br.readLine());
		int N = Integer.valueOf(stringToken.nextToken());
		int M = Integer.valueOf(stringToken.nextToken());
		int[] lectures = new int[N];
		stringToken = new StringTokenizer(br.readLine());

		int st = 0;
		int ed = 0;
		for(int i = 0; i<N; i++) {
			lectures[i] = Integer.valueOf(stringToken.nextToken());
			st = Math.max(st, lectures[i]);
			ed += lectures[i];
		}
		
		while(st <= ed) {
			int mid = (st+ed)/2;
			if(Count(lectures, mid) > M) {
				st = mid + 1;
			}
			else {
				ed = mid - 1;
			}
		}
		System.out.print(st);
	}
	private static int Count(int[] lect, int mid) {
		int count = 0;
		int sum = 0;
		for(int i : lect) {
			if(sum+i > mid) {
				sum = 0;
				count++;
			}
			sum += i;
		}
		if(sum != 0) count++;
		return count;
	}
}
```
배열 내에서 값을 찾는 것은 아주 기본적인 이진 탐색의 형태이고, 이처럼 응용할 수 있다.</br>

기본적인 이진 탐색의 형태
```
public static int binarySearch(int[] arr, int start, int end, int key) {
	int low = start;
	int high = end - 1;

	while(low <= high) {
		int mid = (low + high) >> 1;
		int midVal = arr[mid];
		if (midVal < key) {
			low = mid + 1;
		} else if (midVal == key){
			return mid;
		}
		else {
			high = mid - 1;
		}
	}

	//못찾았을 때
	//return -(high + 2); 와 같음
	return -(low + 1);
}
```

## Lower Bouond</br>
같은 값을 저장하는 요소가 여럿이라면 그 중 가장 작은 값을 반환하는 형태의 코드다.
```
public static int lowerBound(int[] arr, int start, int end, int key){
	int low = start;
	int high = end;

	while (low <= high){
		int mid = (low + high) >> 1;
		int midVal = arr[mid];
		if(midVal < key)        low = mid + 1;
//			else if(midVal == key)  return mid;
			//같으면 high가 줄어드니까 -> 로우는 안줄어들 -> lower_bound 역할
		else                    high = mid - 1;
	}

	return low;
}
```

## Upper Bound
같은 값을 저장하는 요소가 여럿이라면 그 중 가장 큰 값을 반환하는 형태의 코드다.
```
public static int upperBound(int[] arr, int start, int end, int key) {
	int low = start;
	int high = end;

	while (low <= high) {
		int mid = (low + high) >> 1;
		int midVal = arr[mid];
		if(midVal > key)    high = mid - 1;
		//			else if(midVal == key)  return mid;
		//같으면 low가 커지니 -> upper_bound 역할
		else                low = mid + 1;
	}

	return high;
}
```