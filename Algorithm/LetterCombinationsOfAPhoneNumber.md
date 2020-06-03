# Letter Combinations of a Phone Number

## 설명

- [Link](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)

## 풀이

휴대폰 자판에 번호를 입력하면 번호 별로 배정되어 있는 알파벳들을 순차적으로 각각 매칭시킨 값들을 반환하는 문제이다. 매핑시킨다는 것까지는 알았으나 일일히 loop를 돌리면서 반환값을 구하려고 했다. 그럼 길이가 길어질수록 loop의 depth가 깊어져 성능상으로 좋지 못하다. 그래서 재귀를 통해 푼 해법이 참 기발하다. 처음 loop를 돌 때는 3번 돌지만 재귀를 활용해 다음 depth에서 해당 값이 나올 때까지 돌리고 순차적으로 넘어가는 방법이다. 멋있다.

```js
var letterCombinations = function (digits) {
  if (digits.length === 0) return [];

  const map = {
    2: "abc",
    3: "def",
    4: "ghi",
    5: "jkl",
    6: "mno",
    7: "pqrs",
    8: "tuv",
    9: "wxyz",
  };

  let res = [];
  function go(i, s) {
    if (i === digits.length) {
      res.push(s);
      return;
    }
    for (let c of map[digits[i]]) {
      go(i + 1, s + c);
    }
  }

  go(0, "");
  return res;
};
```
