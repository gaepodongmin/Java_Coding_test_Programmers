# 나머지가 1이 되는 수 찾기

## 문제 링크

[프로그래머스 - 나머지가 1이 되는 수 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/87389)

## 내 답

```java
class Solution {
    public int solution(int n) {
        int answer = 0;

        for (int i = 2; i < n; i++) {
            if (n % i == 1) {
                return i;
            }
        }

        return answer;
    }
}
```

## 내 답 풀이

`2`부터 차례대로 숫자를 증가시키면서 `n`을 나눈 나머지가 `1`인지 확인했다.

가장 작은 수부터 검사하기 때문에 조건을 처음 만족하는 `i`가 정답이 된다.

## 더 좋은 답

```java
class Solution {
    public int solution(int n) {
        for (int i = 2; i < n; i++) {
            if ((n - 1) % i == 0) {
                return i;
            }
        }

        return -1;
    }
}
```

## 왜 더 좋은가?

`n % i == 1`이라는 조건은 `(n - 1) % i == 0`과 같다.

따라서 `n - 1`의 가장 작은 약수를 찾는 문제로 생각할 수 있어 문제의 원리를 더 명확하게 표현한다.

또한 사용하지 않는 `answer` 변수를 제거해 코드가 더 간결하다.

## 사용한 알고리즘

* 완전 탐색
* 약수 찾기
* 시간 복잡도: `O(N)`
