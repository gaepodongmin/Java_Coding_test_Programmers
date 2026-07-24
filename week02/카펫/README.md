# 카펫

## 문제 링크

https://school.programmers.co.kr/learn/courses/30/lessons/42842

## 내 답

```java
class Solution {
    public int[] solution(int brown, int yellow) {
        int total = brown + yellow;

        for (int h = 3; h <= total / h; h++) {
            if (total % h == 0) {
                int w = total / h;

                if ((w - 2) * (h - 2) == yellow) {
                    return new int[]{w, h};
                }
            }
        }

        return new int[]{};
    }
}
```

## 내 답 풀이

갈색 격자와 노란색 격자의 합은 카펫 전체 넓이이므로 `total`에 저장했다.

카펫의 세로 길이 `h`를 `3`부터 증가시키면서 전체 넓이의 약수인지 확인했다.

* `total % h == 0`이면 가로 길이 `w`는 `total / h`이다.
* 테두리 한 줄을 제외한 내부 크기는 `(w - 2) × (h - 2)`이다.
* 내부 넓이가 `yellow`와 같으면 해당 가로와 세로 길이를 반환한다.

`h <= total / h` 조건을 사용해 세로 길이가 가로 길이보다 커지는 경우는 확인하지 않았다.

## 더 좋은 답

```java
class Solution {
    public int[] solution(int brown, int yellow) {
        for (int height = 3; height * height <= brown + yellow; height++) {
            int total = brown + yellow;

            if (total % height == 0) {
                int width = total / height;

                if (2 * width + 2 * height - 4 == brown) {
                    return new int[]{width, height};
                }
            }
        }

        return new int[0];
    }
}
```

## 왜 더 좋은가?

갈색 격자가 카펫의 테두리라는 점을 직접 이용해 다음 식으로 확인했다.

```java
2 * width + 2 * height - 4
```

가로와 세로의 테두리를 모두 더한 뒤, 네 모서리가 중복 계산되므로 `4`를 빼면 갈색 격자의 개수가 된다.

기존 답은 노란색 영역을 기준으로 확인하고, 더 좋은 답은 갈색 테두리를 기준으로 확인한다. 두 풀이의 시간 복잡도는 같으며 기존 답도 충분히 좋은 풀이이다.

## 사용한 알고리즘

* 완전 탐색
* 약수 탐색
* 수학
* 시간 복잡도: `O(√N)`
