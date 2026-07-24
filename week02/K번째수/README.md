# K번째수

## 문제 링크

https://school.programmers.co.kr/learn/courses/30/lessons/42748

## 내 답

```java
import java.util.Arrays;

class Solution {
    public int[] solution(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];

        for (int c = 0; c < commands.length; c++) {
            int i = commands[c][0];
            int j = commands[c][1];
            int k = commands[c][2];

            int[] slice = Arrays.copyOfRange(array, i - 1, j);

            Arrays.sort(slice);
            answer[c] = slice[k - 1];
        }

        return answer;
    }
}
```

## 내 답 풀이

각 `command`에서 `i`, `j`, `k` 값을 꺼낸 뒤 다음 과정을 반복했다.

* `Arrays.copyOfRange()`을 사용해 배열의 `i`번째부터 `j`번째까지 자른다.
* 잘라낸 배열을 오름차순으로 정렬한다.
* 정렬된 배열의 `k`번째 값을 `answer`에 저장한다.

배열의 인덱스는 `0`부터 시작하므로 `i - 1`, `k - 1`로 계산했다.

## 더 좋은 답

```java
import java.util.Arrays;

class Solution {
    public int[] solution(int[] array, int[][] commands) {
        return Arrays.stream(commands)
                .mapToInt(command -> {
                    int[] slice = Arrays.copyOfRange(
                            array,
                            command[0] - 1,
                            command[1]
                    );

                    Arrays.sort(slice);
                    return slice[command[2] - 1];
                })
                .toArray();
    }
}
```

## 왜 더 좋은가?

별도의 `answer` 배열과 반복문 인덱스를 직접 관리하지 않고, 각 명령의 결과를 바로 배열로 만들 수 있어 코드가 간결하다.

다만 스트림 문법에 익숙하지 않다면 기존 답이 실행 과정을 이해하기 쉽고 가독성도 충분히 좋다.

## 사용한 알고리즘

* 배열 슬라이싱
* 정렬
* 구현
* 시간 복잡도: 각 명령에서 자른 배열의 길이를 `M`이라고 할 때 `O(C × M log M)`
