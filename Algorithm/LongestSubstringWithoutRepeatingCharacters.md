# Longest Substring Without Repeating Characters

## 설명

- [Link](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

## 풀이

내가 푼 방식으로는 테스트케이스는 통과하지만 `Time Limit Exceeded` 로 문제는 통과하지 못했다. for 문을 중첩으로 사용해 input 값이 긴 경우 접근성이 좋지 못했다. `new Set()` 을 활용한 것도 판단 미스였다고 생각한다.

다른 분의 코드를 보니 심플하고 명확했다.

```js
var lengthOfLongestSubstring = function (s) {
  const length = s.length;
  if (length === 0) return 0;
  if (length === 1) return 1;
  const arr = {};
  for (let i = 0; i < length; i++) {
    for (let j = i; j < length; j++) {
      const a = s.substring(i, j + 1);
      if (new Set(a.split("")).size === a.length && !arr[a]) {
        arr[a] = a.length;
      }
    }
  }
  const answer = [];
  for (const key in arr) {
    answer.push(arr[key]);
  }
  return Math.max(...answer);
};
```

다른 분의 코드

```js
var lengthOfLongestSubstring = function (s) {
  let longest = 0;
  let current = "";

  for (let i = 0; i < s.length; i++) {
    current = current.substring(current.indexOf(s[i]) + 1);
    current += s[i];

    if (current.length > longest) {
      longest = current.length;
    }
  }

  return longest;
};
```
