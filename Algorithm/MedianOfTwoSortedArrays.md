# Median of Two Sorted Arrays

## 설명

- [Link](https://leetcode.com/problems/median-of-two-sorted-arrays/)

## 풀이

두 배열의 중앙값을 구하는 문제로 leetcode 는 난이도를 hard 로 정의했지만 자바스크립트로 풀 수 있는 간단한 문제였다고 생각한다.

```js
var findMedianSortedArrays = function (nums1, nums2) {
  const arr = [...nums1, ...nums2].sort((a, b) => a - b);
  const length = arr.length;
  return length % 2 === 1
    ? arr[(length - 1) / 2]
    : (arr[Math.floor(length / 2) - 1] + arr[length / 2]) / 2;
};
```
