# 콜라 문제

## 문제 링크

https://school.programmers.co.kr/learn/courses/30/lessons/132267

## 내 답

```java
class Solution {
    public int solution(int a, int b, int n) {
        int totalCoke = 0;

        while (n >= a) {
            int newCoke = (n / a) * b;
            totalCoke += newCoke;
            n = (n % a) + newCoke;
        }

        return totalCoke;
    }
}
```

## 내 답 풀이

빈 병이 교환 가능한 개수(`a`) 이상일 동안 반복한다.

* `n / a` : 교환 가능한 횟수
* `(n / a) * b` : 새로 받은 콜라 개수
* 받은 콜라를 정답에 누적한다.
* 남은 빈 병(`n % a`)과 새로 받은 콜라를 마신 뒤 생기는 빈 병을 합쳐 다시 반복한다.

더 이상 교환할 수 없으면 반복을 종료하고 총 받은 콜라 개수를 반환한다.

## 더 좋은 답

```java
class Solution {
    public int solution(int a, int b, int n) {
        int answer = 0;

        while (n >= a) {
            int exchange = n / a;
            answer += exchange * b;
            n = exchange * b + n % a;
        }

        return answer;
    }
}
```

## 왜 더 좋은가?

알고리즘은 동일하지만 변수명을 `exchange`처럼 의미가 드러나도록 작성하여 가독성이 좋아졌다.

또한 계산 과정을 단계별로 표현해 코드를 이해하기 쉽다.

## 사용한 알고리즘

* 시뮬레이션
* 반복문(While)
* 시간 복잡도: **O(log N)** (교환 가능한 병의 개수가 반복할수록 감소)
