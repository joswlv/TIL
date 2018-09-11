# 문제

회사원 Demi는 가끔은 야근을 하는데요, 야근을 하면 야근 피로도가 쌓입니다. 야근 피로도는 야근을 시작한 시점에서 남은 일의 작업량을 제곱하여 더한 값입니다.
Demi는 N시간 동안 야근 피로도를 최소화하도록 일할 겁니다.Demi가 1시간 동안 작업량 1만큼을 처리할 수 있다고 할 때, 퇴근까지 남은 N 시간과 각 일에 대한 작업량 works에 대해 야근 피로도를 최소화한 값을 리턴하는 함수 solution을 완성해주세요.

제한 사항
works는 길이 1 이상, 20,000 이하인 배열입니다.
works의 원소는 50000 이하인 자연수입니다.
n은 1,000,000 이하인 자연수입니다.
입출력 예

|works|	n|	result|
|------|----|----|
|[4, 3, 3]|	4|	12|
|[2, 1, 2]|	1	|6|
|[1,1]|	3|0|

입출력 예 설명

입출력 예 1
n=4 일 때, 남은 일의 작업량이 [4, 3, 3] 이라면 야근 지수를 최소화하기 위해 4시간동안 일을 한 결과는 [2, 2, 2]입니다. 이 때 야근 지수는 2^2 + 2^2 + 2^2 = 12 입니다.

입출력 예 2
n=1일 때, 남은 일의 작업량이 [2,1,2]라면 야근 지수를 최소화하기 위해 1시간동안 일을 한 결과는 [1,1,2]입니다. 야근지수는 1^2 + 1^2 + 2^2 = 6입니다.

# 풀이

처음에 works의 max값을 찾기 위해 배열전체를 scan한 것때문에 O(n^2) 시간으로 나와서 효율성 채크에서 탈락했다.
두번째로 생각한 것이 다음과 같다. 배열 전체를 scan 할 필요없이 처음에 works배열을 오름차순으로 정열한뒤 마지막 값부터 읽고 읽은 값의 앞의 값과 비교만 하면 된다.
그럼 계산량이 줄어드는 효과를 가져온다.

```java
import java.util.Arrays;

public class OvertimeWork {
	public static void main(String[] args) {
		System.out.println(solution(4, new int[]{4, 3, 3}));
		System.out.println(solution(3, new int[]{1, 1}));
	}

	public static long solution(int n, int[] works) {
		long answer = 0;
		long checkSum = 0;

    for (int w:works){
			checkSum+=w;
		}
		if (checkSum-n <= 0) {
			return 0;
		}
		Arrays.sort(works);
		int pos;
		for (int i = 0; i < n; i++) {
			for (pos = works.length-1; pos>0; pos--) {
				if (works[pos-1] < works[pos]) {
					break;
				}
			}
			works[pos] -= 1;
		}
		for (int item : works) {
			answer += Math.pow(item, 2);
		}
		return answer;
	}
}
```
