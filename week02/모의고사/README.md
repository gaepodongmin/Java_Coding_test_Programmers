# 모의고사

## 문제 링크

https://school.programmers.co.kr/learn/courses/30/lessons/42840

## 내 답

```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public int[] solution(int[] answers) {
        int[] p1 = {1, 2, 3, 4, 5};
        int[] p2 = {2, 1, 2, 3, 2, 4, 2, 5};
        int[] p3 = {3, 3, 1, 1, 2, 2, 4, 4, 5, 5};

        int[] score = new int[3];

        for (int i = 0; i < answers.length; i++) {
            if (answers[i] == p1[i % p1.length]) score[0]++;
            if (answers[i] == p2[i % p2.length]) score[1]++;
            if (answers[i] == p3[i % p3.length]) score[2]++;
        }

        int maxScore = Math.max(score[0], Math.max(score[1], score[2]));

        List<Integer> list = new ArrayList<>();

        if (score[0] == maxScore) list.add(1);
        if (score[1] == maxScore) list.add(2);
        if (score[2] == maxScore) list.add(3);

        return list.stream()
                .mapToInt(i -> i)
                .toArray();
    }
}
```

## 내 답 풀이

세 수포자의 반복되는 답안 패턴을 각각 배열로 저장했다.

정답 배열을 순회하면서 나머지 연산을 사용해 각 수포자의 현재 답과 실제 정답을 비교하고, 맞힌 경우 점수를 증가시켰다.

```java
p1[i % p1.length]
```

위와 같이 작성하면 답안 패턴의 길이를 넘어가더라도 처음부터 다시 반복할 수 있다.

점수 중 최댓값을 구한 뒤, 최댓값과 같은 점수를 받은 수포자의 번호를 결과에 추가했다.

## 더 좋은 답

```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public int[] solution(int[] answers) {
        int[][] patterns = {
                {1, 2, 3, 4, 5},
                {2, 1, 2, 3, 2, 4, 2, 5},
                {3, 3, 1, 1, 2, 2, 4, 4, 5, 5}
        };

        int[] scores = new int[patterns.length];

        for (int i = 0; i < answers.length; i++) {
            for (int j = 0; j < patterns.length; j++) {
                if (answers[i] == patterns[j][i % patterns[j].length]) {
                    scores[j]++;
                }
            }
        }

        int maxScore = Math.max(scores[0], Math.max(scores[1], scores[2]));
        List<Integer> result = new ArrayList<>();

        for (int i = 0; i < scores.length; i++) {
            if (scores[i] == maxScore) {
                result.add(i + 1);
            }
        }

        return result.stream()
                .mapToInt(Integer::intValue)
                .toArray();
    }
}
```

## 왜 더 좋은가?

수포자들의 답안 패턴을 2차원 배열로 묶어 중복된 비교 코드를 반복문으로 처리했다.

수포자가 추가되더라도 패턴 배열만 추가하면 되기 때문에 기존 코드보다 확장성과 유지보수성이 좋다.

다만 수포자가 세 명으로 고정된 문제이므로 기존 답도 충분히 간결하고 이해하기 쉽다.

## 사용한 알고리즘

* 완전 탐색
* 배열 순회
* 나머지 연산을 이용한 반복 패턴
* 시간 복잡도: `O(N)`
