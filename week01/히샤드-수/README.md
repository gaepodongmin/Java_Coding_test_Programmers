# 하샤드 수

## 문제 링크

https://school.programmers.co.kr/learn/courses/30/lessons/12947

## 내 답

```java
class Solution {
    public boolean solution(int x) {
        int temp = x;
        int sum = 0;

        while (temp > 0) {
            sum += temp % 10;
            temp /= 10;
        }

        return x % sum == 0;
    }
}
```

## 내 답 풀이

입력받은 숫자 `x`의 각 자릿수를 더한 뒤, `x`가 자릿수의 합으로 나누어떨어지는지 확인했다.

* `temp % 10`으로 마지막 자릿수를 구한다.
* 구한 자릿수를 `sum`에 더한다.
* `temp /= 10`으로 마지막 자릿수를 제거한다.
* 모든 자릿수를 더한 후 `x % sum == 0`의 결과를 반환한다.

## 더 좋은 답

```java
class Solution {
    public boolean solution(int x) {
        int sum = String.valueOf(x)
                        .chars()
                        .map(c -> c - '0')
                        .sum();

        return x % sum == 0;
    }
}
```

## 왜 더 좋은가?

숫자를 문자열로 변환한 뒤 각 문자를 숫자로 바꾸어 합을 계산하기 때문에 자릿수 합을 구하는 과정이 간결하게 표현된다.

다만 문자열 변환과 스트림 처리 비용이 추가되므로 성능과 직관성 측면에서는 기존 답도 충분히 좋다. 코딩테스트에서는 기존 반복문 방식이 오히려 더 효율적이다.

## 사용한 알고리즘

* 자릿수 분리
* 반복문
* 나머지 연산
* 시간 복잡도: `O(log X)`
