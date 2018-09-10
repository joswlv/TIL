# 문제

입력 형식
캐시 크기(cacheSize)와 도시이름 배열(cities)을 입력받는다.
cacheSize는 정수이며, 범위는 0 ≦ cacheSize ≦ 30 이다.
cities는 도시 이름으로 이뤄진 문자열 배열로, 최대 도시 수는 100,000개이다.
각 도시 이름은 공백, 숫자, 특수문자 등이 없는 영문자로 구성되며, 대소문자 구분을 하지 않는다. 도시 이름은 최대 20자로 이루어져 있다.
출력 형식
입력된 도시이름 배열을 순서대로 처리할 때, 총 실행시간을 출력한다.
조건
캐시 교체 알고리즘은 LRU(Least Recently Used)를 사용한다.
cache hit일 경우 실행시간은 1이다.
cache miss일 경우 실행시간은 5이다.
입출력 예제

|캐시크기(cacheSize)|도시이름(cities)|실행시간
|----|----|-----|
|3|[Jeju, Pangyo, Seoul, NewYork, LA, Jeju, Pangyo, Seoul, NewYork, LA]|50|
|3|[Jeju, Pangyo, Seoul, Jeju, Pangyo, Seoul, Jeju, Pangyo, Seoul]|21|
|2|[Jeju, Pangyo, Seoul, NewYork, LA, SanFrancisco, Seoul, Rome, Paris, Jeju, NewYork, Rome]|60|
|5|[Jeju, Pangyo, Seoul, NewYork, LA, SanFrancisco, Seoul, Rome, Paris, Jeju, NewYork, Rome]|52|
|2|[Jeju, Pangyo, NewYork, newyork]|16|
|0|[Jeju, Pangyo, Seoul, NewYork, LA]|25|

# 풀이

```java
public class LRUCacheForKakao {
	public static void main(String[] args) {
		System.out.println(solution(3, new String[]{"Jeju", "Pangyo", "Seoul", "NewYork", "LA", "Jeju", "Pangyo", "Seoul", "NewYork", "LA"}));
	}

	private static int solution(int cacheSize, String[] cities) {
		int answer = 0;
		if (cacheSize == 0) {
			answer = cities.length*5;
		} else {
			LRUCache lruCache = new LRUCache(cacheSize);
			for (String city : cities) {
				String c = city.toLowerCase();
				if (lruCache.get(c).equals("-1")) {
					answer += 5;
				} else {
					answer += 1;
				}
				lruCache.set(c, c);
			}
		}

		return answer;
	}

	public static class LRUCache {
		private Map<String, String> blocks = new HashMap<>();
		private LinkedList<String> bru = new LinkedList<>();
		private int capacity;
		private int length;

		public LRUCache(int capacity) {
			this.capacity = capacity;
			this.length = 0;
		}

		public String get(String key) {
			String value = blocks.get(key);
			if (value != null) {
				bru.remove(value);
				bru.addFirst(value);
				return value;
			}
			return "-1";
		}

		public void set(String key, String value) {
			if (blocks.containsKey(key)) {
				bru.remove(blocks.get(key));
				blocks.put(key, value);
			} else {
				if (length >= capacity) {
					blocks.remove(bru.removeLast());
					length--;
				}
				length++;
				blocks.put(key, value);
			}
			bru.addFirst(value);
		}

	}
}
```
