# 3Sum

## 설명

- [Link](https://leetcode.com/problems/3sum/)

## 풀이

배열 중 3 요소의 합이 0이 되는 요소들을 배열로 반환하는 문제이다. 처음 풀이는 길이가 긴 배열에서 시간초과로 통과하지 못했다. 그 중 이해되는 다른 분의 풀이 아래에 첨부했다. 먼저 정렬을 한 다음, 두 요소의 합의 크기를 비교해 세 요소 중 첫 번째 요소보다 두 요소의 합이 클 경우 총 배열의 길이를 왼쪽으로 당기고 합이 작을 경우 오른쪽으로 당겨 모든 요소를 돌지 않고 시간을 단축시켰다. 최고의 예제인지 모르겠다.

```js
var threeSum = function (nums) {
  if (nums.length < 3) return [];
  const arr = [];
  const hashMap = {};
  let index = 0;
  for (var i = 0; i < nums.length; i++) {
    for (var j = i + 1; j < nums.length; j++) {
      for (var k = j + 1; k < nums.length; k++) {
        if (nums[i] + nums[j] + nums[k] === 0) {
          const [a, b, c] = [nums[i], nums[j], nums[k]].sort();
          const abc = `${a}-${b}-${c}`;
          if (!hashMap[abc]) {
            arr.push([a, b, c]);
            hashMap[abc] = true;
          }
        }
      }
    }
  }
  return arr;
};
```

```js
var threeSum = function (nums) {
  if (nums.length < 3) return [];
  const arr = nums.sort((a, b) => a - b);
  const ans = {};
  for (let i = 0; i < arr.length; i++) {
    const target = 0 - arr[i];
    let l = i + 1;
    let r = arr.length - 1;
    if (target === 0 && arr[l] === 0 && arr[r] === 0 && l !== r) {
      const sol = [arr[i], arr[l], arr[r]];
      ans[sol] = 1;
      continue;
    }
    while (l < r) {
      const sum = arr[l] + arr[r];
      if (sum === target) {
        const sol = [arr[i], arr[l], arr[r]];
        const sorted = sol.sort();
        ans[sorted] = 1;
      }
      if (sum < target) {
        l++;
      } else {
        r--;
      }
    }
  }
  return Object.keys(ans).map((k) => k.split(",").map((k) => Number(k)));
};
```
