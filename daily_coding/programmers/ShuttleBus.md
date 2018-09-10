# 문제

이 문제에서는 편의를 위해 셔틀은 다음과 같은 규칙으로 운행한다고 가정하자.

셔틀은 09:00부터 총 n회 t분 간격으로 역에 도착하며, 하나의 셔틀에는 최대 m명의 승객이 탈 수 있다.
셔틀은 도착했을 때 도착한 순간에 대기열에 선 크루까지 포함해서 대기 순서대로 태우고 바로 출발한다. 예를 들어 09:00에 도착한 셔틀은 자리가 있다면 09:00에 줄을 선 크루도 탈 수 있다.
일찍 나와서 셔틀을 기다리는 것이 귀찮았던 콘은, 일주일간의 집요한 관찰 끝에 어떤 크루가 몇 시에 셔틀 대기열에 도착하는지 알아냈다. 콘이 셔틀을 타고 사무실로 갈 수 있는 도착 시각 중 제일 늦은 시각을 구하여라.

단, 콘은 게으르기 때문에 같은 시각에 도착한 크루 중 대기열에서 제일 뒤에 선다. 또한, 모든 크루는 잠을 자야 하므로 23:59에 집에 돌아간다. 따라서 어떤 크루도 다음날 셔틀을 타는 일은 없다.

입력 형식
셔틀 운행 횟수 n, 셔틀 운행 간격 t, 한 셔틀에 탈 수 있는 최대 크루 수 m, 크루가 대기열에 도착하는 시각을 모은 배열 timetable이 입력으로 주어진다.

0 ＜ n ≦ 10
0 ＜ t ≦ 60
0 ＜ m ≦ 45
timetable은 최소 길이 1이고 최대 길이 2000인 배열로, 하루 동안 크루가 대기열에 도착하는 시각이 HH:MM 형식으로 이루어져 있다.
크루의 도착 시각 HH:MM은 00:01에서 23:59 사이이다.
출력 형식
콘이 무사히 셔틀을 타고 사무실로 갈 수 있는 제일 늦은 도착 시각을 출력한다. 도착 시각은 HH:MM 형식이며, 00:00에서 23:59 사이의 값이 될 수 있다.

입출력 예제

|n|t|m|timetable|answer|
|----|---|--|---|---|
|1|1|5|[08:00, 08:01, 08:02, 08:03]|09:00|
|2|10|2|[09:10, 09:09, 08:00]|09:09|
|2|1|2|[09:00, 09:00, 09:00, 09:00]|08:59|
|1|1|5|[00:01, 00:01, 00:01, 00:01, 00:01]|00:00|
|1|1|1|[23:59]|09:00|
|10|60|45|[23:59,23:59, 23:59, 23:59, 23:59, 23:59, 23:59, 23:59, 23:59, 23:59, 23:59, 23:59, 23:59, 23:59, 23:59, 23:59]|18:00|


# 풀이

```java
import java.util.Arrays;
import java.util.OptionalInt;

public class ShuttleBus {
	public static void main(String[] args) {
		System.out.println(solution(2,10,2,new String[]{"09:10", "09:09", "08:00"}));
		System.out.println(solution(1,1,5,new String[]{"00:01", "00:01", "00:01", "00:01", "00:01"}));
		System.out.println(solution(2,1,2,new String[]{"09:00", "09:00", "09:00", "09:00"}));
	}

	//셔틀 운행 횟수 n, 셔틀 운행 간격 t, 한 셔틀에 탈 수 있는 최대 크루 수 m
	public static String solution(int n, int t, int m, String[] timetable) {
		int answer = timerFrom9(n, t, m, changeTime(timetable));
		return toAnswer(answer);
	}

	//00시로부터 몇분 떨어져있나
	public static int[] changeTime(String[] timetable) {
		int[] minTable = Arrays.stream(timetable).filter(t -> !t.equals("23:59")).mapToInt(t -> {
					String[] sp = t.split(":");
					return Integer.parseInt(sp[0]) * 60 + Integer.parseInt(sp[1]);
				}
		).toArray();
		return minTable;
	}

	public static String toAnswer(int answer) {
		return String.format("%02d:%02d",answer/60,answer%60);
	}

	public static int timerFrom9(int n, int t, int m, int[] timetable) {
		int startTime = 540;
		int endTime = 540 + t;
		int boardingBusUser = 0;
		int beforeStrartTimeUser = 0;
		int answerTime = 0;
		//운행횟수
		for (int i = 0; i < n; i++) {
			for (int memberTime : timetable) {
				if (memberTime <= 540) {
					beforeStrartTimeUser ++;
				}
				if (startTime <= memberTime && memberTime < endTime) {
					beforeStrartTimeUser--;
					boardingBusUser++;
				}
			}
			if (boardingBusUser < m) {
				answerTime = startTime;
			} else {
				answerTime = startTime - 1;
			}
			if (beforeStrartTimeUser >= m) {
				OptionalInt lowest = Arrays.stream(timetable).min();
				answerTime = lowest.getAsInt() - 1;
			}
			startTime += t;
			endTime += t;
		}

		return answerTime;
	}
}
```
