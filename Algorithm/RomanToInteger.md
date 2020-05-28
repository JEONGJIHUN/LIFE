# Roman to Integer

## 설명

- [Link](https://leetcode.com/problems/roman-to-integer/)

## 풀이

- 기존의 roman set 을 roman1 과 roman2 로 나눠 roman2 부터 문자열을 확인하고 roman2 의 key 값을 찾아내고 필러링한값을 다 더하고, 필터된 문자열을 roman1 으로 key 값을 매칭한 뒤 다 더해 값을 구했다.

```js
function romanToInt(s) {
  const roman1 = {
    M: 1000,
    D: 500,
    C: 100,
    L: 50,
    X: 10,
    V: 5,
    I: 1,
  };
  const roman2 = {
    CM: 900,
    CD: 400,
    XC: 90,
    XL: 40,
    IX: 9,
    IV: 4,
  };

  let copiedS = s;
  const filteredRoman2Key = Object.keys(roman2).map((el) => {
    if (copiedS.includes(el)) {
      copiedS = copiedS.replace(el, "");
      return el;
    } else {
      return 0;
    }
  });
  const roman2Answer = filteredRoman2Key
    .filter(Boolean)
    .map((el) => roman2[el])
    .reduce((acc, curr) => acc + curr, 0);
  const roman1Answer = aa
    .split("")
    .map((el) => roman1[el])
    .reduce((acc, curr) => acc + curr, 0);
  return roman1Answer + roman2Answer;
}
```
