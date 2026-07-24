# 콜라츠 추측

## 문제 링크

https://school.programmers.co.kr/learn/courses/30/lessons/12943

## 내 답

```java
class Solution {
    public int solution(int num) {
        long n = num;
        int count = 0;

        while (n != 1) {
            if (count >= 500) {
                return -1;
            }

            if (n % 2 == 0) {
                n /= 2;
            } else {
                n = n * 3 + 1;
            }

            count++;
        }

        return count;
    }
}
```

## 내 답 풀이

입력받은 숫자가 `1`이 될 때까지 다음 과정을 반복했다.

* 짝수이면 `2`로 나눈다.
* 홀수이면 `3`을 곱한 뒤 `1`을 더한다.
* 연산을 수행할 때마다 `count`를 증가시킨다.
* 연산 횟수가 500번 이상이면 `-1`을 반환한다.

계산 과정에서 정수 범위를 넘어갈 수 있으므로 `num`을 `long` 타입으로 변환해 사용했다.

## 더 좋은 답

```java
class Solution {
    public int solution(int num) {
        long n = num;

        for (int count = 0; count < 500; count++) {
            if (n == 1) {
                return count;
            }

            n = n % 2 == 0 ? n / 2 : n * 3 + 1;
        }

        return -1;
    }
}
```

## 왜 더 좋은가?

반복 횟수가 최대 500번이라는 조건을 `for`문의 종료 조건으로 직접 표현해 코드가 더 간결하다.

또한 짝수와 홀수에 따른 계산을 삼항 연산자로 작성해 중복되는 코드 구조를 줄였다.

다만 가독성을 중요하게 생각한다면 기존 답처럼 `if-else`로 작성하는 것도 충분히 좋은 방법이다.

## 사용한 알고리즘

* 시뮬레이션
* 반복문
* 조건 분기
* 시간 복잡도: `O(500)`, 상수 시간
