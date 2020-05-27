# Integer to Roman

## 설명

- [Link](https://leetcode.com/problems/integer-to-roman/)

## 풀이

미리 나올 수 있는 roman 값들을 정의해 두고 정의한 value 값을 나눈 몫을 차감하는 식으로 진행했다.

```js
function integerToRoman(num) {
  const roman = {
    M: 1000,
    CM: 900,
    D: 500,
    CD: 400,
    C: 100,
    XC: 90,
    L: 50,
    XL: 40,
    X: 10,
    IX: 9,
    V: 5,
    IV: 4,
    I: 1,
  };
  let number = num;
  const answer = Object.entries(roman).map(([key, value]) => {
    const quotient = Math.floor(number / value);
    number -= quotient * value;
    return key.repeat(quotient);
  });

  return answer.filter(Boolean).join("");
}
```
