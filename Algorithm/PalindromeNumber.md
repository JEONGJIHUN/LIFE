# Palindrome Number

## 설명

- [Link](https://leetcode.com/problems/palindrome-number/)

## 풀이

파라미터로 들어오는 정수를 역순으로 배열했을 때 동일한 값이 반환 되어야하는 문제이다. 나는 처음 접근을 각각 처음 배열값과 마지막 배열 값들을 하나하나 비교했다. 하지만 두 번째 방식은 20줄의 코드를 단 한 줄로 표현했다. 성능적인 측면에서는 크게 차이나지 않았다. 차이를 두자면 런타임에서 30ms 정도 차이나는 정도였다.
드는 생각은 기존 메소드를 잘 활용해야겠다.

```js
var isPalindrome = function (x) {
  if (x < 0) return false;
  const str = String(x);
  const oddLength = (str.length - 1) / 2;
  const evenLength = str.length / 2;
  const odd = str.length % 2 === 1;
  const arr = [];
  for (let i = 0; i < evenLength; i++) {
    if (str[i] === str[str.length - i - 1]) {
      if (odd) {
        if (i != oddLength) {
          arr.push(1);
        }
      } else {
        arr.push(1);
      }
    } else {
      return false;
    }
  }
  return arr.length === (odd ? oddLength : evenLength);
};
```

```js
var isPalindrome = function (x) {
   return x === Number(String(x).split("").reverse().join(""));
};
```