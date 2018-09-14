# 문제

전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려 합니다.
전화번호가 다음과 같을 경우, 구조대 전화번호는 영석이의 전화번호의 접두사입니다.

구조대 : 119
박준영 : 97 674 223
지영석 : 11 9552 4421
전화번호부에 적힌 전화번호를 담은 배열 phoneBook 이 solution 함수의 매개변수로 주어질 때,
어떤 번호가 다른 번호의 접두어인 경우가 있으면 false를 그렇지 않으면 true를 return 하도록 solution 함수를 작성해주세요.

제한 사항
phoneBook의 길이는 1 이상, 100 이하입니다.
각 전화번호의 길이는 1 이상, 20 이하입니다.

입출력 예제

|phoneBook|	return|
|-------|------|
|[119, 97674223, 1195524421]	|false|
|[123,456,789]|	true|
|[12,123,1235,567,88]	|false|

입출력 예 설명

입출력 예 #1
앞에서 설명한 예와 같습니다.

입출력 예 #2
한 번호가 다른 번호의 접두사인 경우가 없으므로, 답은 true입니다.

입출력 예 #3
첫 번째 전화번호, “12”가 두 번째 전화번호 “123”의 접두사입니다. 따라서 답은 false입니다.

# 풀이

```java
import java.util.Arrays;

public class PhoneNumber {
	public static void main(String[] args) {
		System.out.println(solution(new String[]{"119", "97674223", "1195524421"}));
		System.out.println(solution(new String[]{"123", "456", "789"}));
		System.out.println(solution(new String[]{"1243", "12", "135", "567", "88"}));
		System.out.println(solution(new String[]{"12", "23", "135", "99567", "88"}));

	}

	public static boolean solution(String[] phoneBook) {
		boolean answer = true;
		int phoneBookSize = phoneBook.length;
		Arrays.sort(phoneBook);
		for (int i = 0; i < phoneBookSize-1; i++) {
			int now = phoneBook[i].length();
			int next = phoneBook[i+1].length();
			if (now < next) {
				if (phoneBook[i+1].indexOf(phoneBook[i]) > -1) {
					return false;
				}
			}
		}
		return answer;
	}
}
```
