# 3Sum Closet

## 설명

- [Link](https://leetcode.com/problems/3sum-closest/)

## 풀이

배열 중 3 요소의 합이 target과 같거나 혹은 같은 값이 없다면, 가장 근접한 값을 반환하는 문제이다.
다른 분의 풀이 아래에 첨부했다. 타겟과 3sum 의 차이를 구해 가장 작은 차이를 구하는 것이 기존의 3sum 문제와의 차이점이다.
그래도 이해가 되니 재미가 붙는다. 다음 번엔 되도록 해답을 보지 않고 풀어버려야겠다.

```js
var threeSumClosest = function (nums, target) {
  const sortedArr = nums.sort((a, b) => a - b);
  let sum = sortedArr[0] + sortedArr[1] + sortedArr[2];
  let distance = Math.abs(sum - target);
  const length = sortedArr.length;

  for (let i = 0; i < length; i++) {
    const num1 = sortedArr[i];
    let l = i + 1;
    let r = length - 1;

    while (l < r) {
      let num2 = sortedArr[l];
      let num3 = sortedArr[r];
      let diff = num1 + num2 + num3 - target;
      if (diff === 0) {
        return target;
      } else if (diff > 0) {
        r--;
      } else {
        l++;
      }

      if (distance > Math.abs(diff)) {
        distance = Math.abs(diff);
        sum = num1 + num2 + num3;
      }
    }
  }
  return sum;
};
```
