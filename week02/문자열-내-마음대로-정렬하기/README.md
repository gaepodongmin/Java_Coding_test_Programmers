# 문자열 내 마음대로 정렬하기

## 문제 링크

https://school.programmers.co.kr/learn/courses/30/lessons/12915

## 내 답

```java
import java.util.Arrays;

class Solution {
    public String[] solution(String[] strings, int n) {
        Arrays.sort(strings, (s1, s2) -> {
            if (s1.charAt(n) == s2.charAt(n)) {
                return s1.compareTo(s2);
            }

            return Character.compare(s1.charAt(n), s2.charAt(n));
        });

        return strings;
    }
}
```

## 내 답 풀이

`Arrays.sort()`에 람다식을 사용해 문자열 배열의 정렬 기준을 직접 지정했다.

먼저 두 문자열의 `n`번째 문자를 비교한다.

* `n`번째 문자가 다르면 해당 문자를 기준으로 오름차순 정렬한다.
* `n`번째 문자가 같으면 `compareTo()`를 사용해 문자열 전체를 사전순으로 정렬한다.

## 더 좋은 답

```java
import java.util.Arrays;
import java.util.Comparator;

class Solution {
    public String[] solution(String[] strings, int n) {
        Arrays.sort(
                strings,
                Comparator.comparingInt((String s) -> s.charAt(n))
                          .thenComparing(Comparator.naturalOrder())
        );

        return strings;
    }
}
```

## 왜 더 좋은가?

`Comparator.comparingInt()`와 `thenComparing()`을 사용해 첫 번째 정렬 기준과 두 번째 정렬 기준을 명확하게 분리했다.

따라서 `if`문 없이도 다음 정렬 조건을 쉽게 확인할 수 있다.

1. `n`번째 문자 기준 정렬
2. 문자가 같으면 문자열 전체 기준 사전순 정렬

다만 기존 답도 정렬 조건이 명확하고 충분히 좋은 풀이이다.

## 사용한 알고리즘

* 정렬
* 사용자 정의 비교 함수
* 사전순 비교
* 시간 복잡도: `O(N log N)`
