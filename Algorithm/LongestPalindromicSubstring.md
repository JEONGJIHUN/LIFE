# Longest Palindromic Substring

## 설명

- [Link](https://leetcode.com/problems/longest-palindromic-substring/)

## 풀이

엉터리로 접근하는 바람에 통과하지 못했다. 결국 다른 분들의 풀이를 보았는데 두가지 방법이 있었다.
dynamic programming 접근법과 Manacher algorithm 을 사용하는 방법이 있다. 아래의 레퍼런스를 확인하면 이해할 수 있을 것이다.

예를 들어 하위 문자열 (2,4) "bad"가 회문이 아니기 때문에 문자열 "babad" dp [2][4]가 false 인 것으로 간주하십시오.

isPalindrome()을 완전히 제거하는 대신 간단한 로직을 작성하여 테이블을 채웁니다. 동일한 중첩 루프가 여기에 있지만 논리가 변경되어 논리를 다음과 같이 설명할 수 있습니다.

사례 1 : i === j

- 문자열의 모든 단일 문자는 회문입니다. 따라서 dp [i][j]는 true입니다.

사례 2 : j-i === 1

- s[i] == s[j]이면 dp [i][j]가 true 인 경우 한 번에 두 문자를 확인합니다.

사례 3 : j-i >= 2

- "aba"s [0] = s [2]를 고려하므로 dp [i][j]는 true입니다. s [i] == s [j]이지만 j-i> = 2 인 경우, dp [i][j] = dp [i + 1][j-1]. 이제 i + 1, j-1 좌표는 말 그대로 첫 번째 문자와 마지막 문자를 제거합니다. 이미 같은 문자이기 때문에 문자가 없는 문자열이 여전히 회문인지 아닌지 알고 싶습니다. 이 결과는 위의 경우 중 하나이거나이 경우에도 결과가 이미 계산 된 것입니다.

```js
var longestPalindrome = function (s) {
  let maxlen = 1,
    result = s[0],
    start = 0,
    dp = [];
  for (let i = 0; i < s.length; i++) {
    dp.push([]);
  }
  for (let i = 0; i < s.length; i++) {
    for (let j = 0; j < i; j++) {
      if (s[i] === s[j]) {
        if (i - j <= 2) {
          if (i - j + 1 > maxlen) {
            start = j;
            maxlen = i - j + 1;
          }
          dp[j][i] = true;
        } else if (dp[j + 1][i - 1]) {
          if (i - j + 1 > maxlen) {
            start = j;
            maxlen = i - j + 1;
          }
          dp[j][i] = true;
        }
      }
    }
  }
  return s.substr(start, maxlen);
};
```

Manacher algorithm 을 사용한다면 시간복잡도가 O(n) 으로 줄일 수 있다.

```js
var longestPalindrome = function (s) {
  s = "#" + s.split("").join("#") + "#";
  let maxRight = 0,
    pos = 0,
    RL = new Array(s.length),
    center = 0,
    maxR = 1;
  for (let i = 0; i < s.length; i++) {
    if (i < maxRight) {
      RL[i] = Math.min(RL[2 * pos - i], maxRight - i);
    } else {
      RL[i] = 1;
    }
    while (
      i + RL[i] < s.length &&
      i - RL[i] >= 0 &&
      s[i + RL[i]] === s[i - RL[i]]
    ) {
      RL[i] += 1;
    }
    if (RL[i] + i - 1 > maxRight) {
      maxRight = RL[i] + i - 1;
      pos = i;
    }
    if (RL[i] > maxR) {
      center = i;
      maxR = RL[i];
    }
  }
  return s
    .slice(center - maxR + 1, center + maxR)
    .split("#")
    .join("");
};
```

## Ref

- https://www.crocus.co.kr/1075
- https://iq.opengenus.org/longest-palindromic-substring-dp/
- https://namnamseo.tistory.com/entry/%EC%A0%84%EC%B2%B4-%EB%AC%B8%EC%9E%90%EC%97%B4%EC%97%90%EC%84%9C-palindrome%EC%9D%98-%EA%B0%AF%EC%88%98-%EC%84%B8%EA%B8%B0-ON
