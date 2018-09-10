# 문제

1. 다트 게임은 총 3번의 기회로 구성된다.
2. 각 기회마다 얻을 수 있는 점수는 0점에서 10점까지이다.
3. 점수와 함께 Single(S), Double(D), Triple(T) 영역이 존재하고 각 영역 당첨 시 점수에서 1제곱, 2제곱, 3제곱 (점수1 , 점수2 , 점수3 )으로 계산된다.
4. 옵션으로 스타상(\*) , 아차상(#)이 존재하며 스타상(\*) 당첨 시 해당 점수와 바로 전에 얻은 점수를 각 2배로 만든다. 아차상(#) 당첨 시 해당 점수는 마이너스된다.
5. 스타상(\*)은 첫 번째 기회에서도 나올 수 있다. 이 경우 첫 번째 스타상(\*)의 점수만 2배가 된다. (예제 4번 참고)
6. 스타상(\*)의 효과는 다른 스타상(\*)의 효과와 중첩될 수 있다. 이 경우 중첩된 스타상(\*) 점수는 4배가 된다. (예제 4번 참고)
7. 스타상(\*)의 효과는 아차상(#)의 효과와 중첩될 수 있다. 이 경우 중첩된 아차상(#)의 점수는 -2배가 된다. (예제 5번 참고)
8. Single(S), Double(D), Triple(T)은 점수마다 하나씩 존재한다.
9. 스타상(\*), 아차상(#)은 점수마다 둘 중 하나만 존재할 수 있으며, 존재하지 않을 수도 있다.
10. 0~10의 정수와 문자 S, D, T, \*, #로 구성된 문자열이 입력될 시 총점수를 반환하는 함수를 작성하라.

입력 형식
점수|보너스|[옵션]으로 이루어진 문자열 3세트.
예) 1S2D*3T

점수는 0에서 10 사이의 정수이다.
보너스는 S, D, T 중 하나이다.
옵선은 \*이나 # 중 하나이며, 없을 수도 있다.
출력 형식
3번의 기회에서 얻은 점수 합계에 해당하는 정수값을 출력한다.
예) 37

입출력 예제

|예제|dartResult|answer|설명|
|---|----|----|---|
|1|1S2D*3T|37|11 * 2 + 22 * 2 + 33|
|2|1D2S#10S|9|12 + 21 * (-1) + 101|
|3|1D2S0T|3|12 + 21 + 03|
|4|1S*2T*3S|23|11 * 2 * 2 + 23 * 2 + 31|
|5|1D#2S*3S|5|12 * (-1) * 2 + 21 * 2 + 31|
|6|1T2D3D#|-4|13 + 22 + 32 * (-1)|
|7|1D2S3T*|59|12 + 21 * 2 + 33 * 2|

# 풀이

```java
import java.util.HashMap;

public class DartGame {
	public static void main(String[] args) {
		System.out.println(solution("1S2D*3T"));
		System.out.println(solution("1D2S#10S"));
		System.out.println(solution("1D2S0T"));
		System.out.println(solution("1S*2T*3S"));
		System.out.println(solution("1D#2S*3S"));
		System.out.println(solution("1T2D3D#"));
		System.out.println(solution("1D2S3T*"));
	}

	public static int solution(String dartResult) {
		int answer = 0;
		HashMap<String, Integer> bonusArea = new HashMap<>();
		bonusArea.put("S", 1);
		bonusArea.put("D", 2);
		bonusArea.put("T", 3);
		int[] roundResult = new int[3];
		int starCount = 0;
		int minusCount = 0;
		int dartScore = 0;
		int round = 0;

		for (int i = 0; i < dartResult.length(); i++) {
			char pointChar = dartResult.charAt(i);
			if (pointChar == '1' && dartResult.charAt(i + 1) == '0') {
				dartScore = 10;
				i ++;
			} else if (!bonusArea.containsKey(String.valueOf(pointChar)) && pointChar != '*' && pointChar != '#') {
				dartScore = Integer.parseInt(String.valueOf(pointChar));
			}

			if (bonusArea.containsKey(String.valueOf(pointChar))) {
				char option = ' ';
				if (i != dartResult.length()-1) {
					option = dartResult.charAt(i + 1);
				}
				if (option == '*') {
					if (round == 0) {
						roundResult[round] = (int) (Math.pow(dartScore, bonusArea.get(String.valueOf(pointChar))) * 2);
						starCount += 1;
					} else {
						if (starCount == 0) {
							roundResult[round] = (int) (Math.pow(dartScore, bonusArea.get(String.valueOf(pointChar))) * 2);
							roundResult[round - 1] = roundResult[round - 1] * 2;
							starCount += 1;
						} else if (starCount >= 1) {
							roundResult[round] = (int) (Math.pow(dartScore, bonusArea.get(String.valueOf(pointChar))) * 2);
							roundResult[round - 1] = roundResult[round - 1] * 2;
							starCount += 1;
						} else if (minusCount >= 1) {
							roundResult[round] = (int) (Math.pow(dartScore, bonusArea.get(String.valueOf(pointChar))) * 2);
							roundResult[round - 1] = roundResult[round - 1] * 2;
						}
					}
					round += 1;
				} else if (option == '#') {
					roundResult[round] = (int) (Math.pow(dartScore, bonusArea.get(String.valueOf(pointChar))) * -1);
					minusCount += 1;
					round += 1;
				} else {
					roundResult[round] = (int) (Math.pow(dartScore, bonusArea.get(String.valueOf(pointChar))));
					round += 1;
				}

			}
		}

		for (int a : roundResult) {
			answer += a;
		}
		return answer;
	}
}
```
