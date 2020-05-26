# Container With Most Water

## 설명

- [Link](https://leetcode.com/problems/container-with-most-water/)

## 풀이

컨테이너에 물을 부었을 때 최대 용량을 구하는 문제이다. 풀이를 보고 배열의 길이를 디스트럭처링 할 수 있겠구나 라고 깨달았고, while 안의 조건문도 쌈박하게 물었다고 생각한다.

```js
var maxArea = function (height) {
  const { length } = height;
  let i = 0;
  let j = length - 1;
  let max = 0;
  while (i < j) {
    const x = j - i;
    const y = height[height[i] < height[j] ? i++ : j--];
    const res = x * y;
    if (res > max) {
      max = res;
    }
  }
  return max;
};
```
