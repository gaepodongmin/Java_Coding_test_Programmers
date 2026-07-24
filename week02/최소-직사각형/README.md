# 최소직사각형

## 문제 링크

https://school.programmers.co.kr/learn/courses/30/lessons/86491

## 내 답

```java
class Solution {
    public int solution(int[][] sizes) {
        int maxW = 0;
        int maxH = 0;

        for (int[] size : sizes) {
            int w = Math.max(size[0], size[1]);
            int h = Math.min(size[0], size[1]);

            maxW = Math.max(maxW, w);
            maxH = Math.max(maxH, h);
        }

        return maxW * maxH;
    }
}
```

## 내 답 풀이

각 명함은 가로와 세로를 회전할 수 있으므로, 두 길이 중 큰 값을 가로로 두고 작은 값을 세로로 두었다.

모든 명함을 순회하면서 다음 값을 구했다.

* 큰 길이 중 최댓값을 `maxW`에 저장
* 작은 길이 중 최댓값을 `maxH`에 저장

마지막에 `maxW * maxH`를 계산해 모든 명함을 넣을 수 있는 가장 작은 지갑의 크기를 구했다.

## 더 좋은 답

```java
class Solution {
    public int solution(int[][] sizes) {
        int width = 0;
        int height = 0;

        for (int[] size : sizes) {
            width = Math.max(width, Math.max(size[0], size[1]));
            height = Math.max(height, Math.min(size[0], size[1]));
        }

        return width * height;
    }
}
```

## 왜 더 좋은가?

별도의 `w`, `h` 변수를 만들지 않고 바로 최댓값을 갱신해 코드가 조금 더 간결하다.

다만 기존 답은 큰 길이와 작은 길이를 변수로 분리해 계산 과정이 더 잘 보이므로 가독성 측면에서는 기존 풀이도 충분히 좋다.

## 사용한 알고리즘

* 완전 탐색
* 그리디
* 최댓값 비교
* 시간 복잡도: `O(N)`
