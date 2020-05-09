# ZigZag Conversion

## 설명

- [Link](https://leetcode.com/problems/zigzag-conversion/)

## 풀이

문제를 풀다보니 알고리즘 접근법이 부족하다고 생각하여 책을 구입해 공부해보려한다. 아래의 풀이를 보며 또 한번 깨달았다. 루프 한 번으로 나머지를 구해 값을 들어갈 해당 위치를 구했다. 문제도 많이 접해봐야겠지만 이러한 접근법을 파악하고 적용하는 것도 중요하다고 생각한다.

```js
var convert = (s, numRows) => {
  if (s.length <= numRows || numRows < 2) return s;
  const arr = Array(numRows).fill("");
  const num = 2 * (numRows - 1);
  for (let i = 0; i < s.length; i++) {
    const pos = i % num || 0;
    arr[pos < numRows ? pos : num - pos] += s[i];
  }
  return arr.join("");
};
```
