# Longest Common Prefix

## 설명

- [Link](https://leetcode.com/problems/longest-common-prefix/)

## 풀이

일단 배열을 정렬해주고 처음 값과 마지막 값을 비교하면 쉽게 구할 수 있는 문제이다.

```js
var longestCommonPrefix = function (strs) {
  if (!strs || strs.length === 0) {
    return "";
  }
  const sortedStrs = strs.sort();
  const firstStr = sortedStrs[0];
  const lastStr = sortedStrs[sortedStrs.length - 1];
  let i = 0;
  while (i < firstStr.length && firstStr[i] === lastStr[i]) {
    i++;
  }
  return firstStr.substring(0, i);
};
```
