# Reverse Integer

## 설명

- [Link](https://leetcode.com/problems/reverse-integer/)

## 풀이

```js
var reverse = function (x) {
  const range = Math.pow(2, 31);
  const answer = Number(String(Math.abs(x)).split("").reverse().join(""));
  return answer >= range - 1 ? 0 : x >= 0 ? answer : -answer;
};
```
