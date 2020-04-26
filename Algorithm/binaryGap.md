# Binary Gap

## 설명

A binary gap within a positive integer N is any maximal sequence of consecutive zeros that is surrounded by ones at both ends in the binary representation of N.

For example, number 9 has binary representation 1001 and contains a binary gap of length 2. The number 529 has binary representation 1000010001 and contains two binary gaps: one of length 4 and one of length 3. The number 20 has binary representation 10100 and contains one binary gap of length 1. The number 15 has binary representation 1111 and has no binary gaps. The number 32 has binary representation 100000 and has no binary gaps.

Write a function:

class Solution { public int solution(int N); }

that, given a positive integer N, returns the length of its longest binary gap. The function should return 0 if N doesn't contain a binary gap.

For example, given N = 1041 the function should return 5, because N has binary representation 10000010001 and so its longest binary gap is of length 5. Given N = 32 the function should return 0, because N has binary representation '100000' and thus no binary gaps.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [1..2,147,483,647].
Copyright 2009–2020 by Codility Limited. All Rights Reserved. Unauthorized copying, publication or disclosure prohibited.

## 풀이

- 처음에 제출한 방식은 toString 을 사용하지 않고 재귀함수를 사용해 이진법으로 변환한 뒤 값을 구해 진행했다. `arr` 에서 제일 처음 숫자가 1일 때를 방지하기 위해 반환되는 모든 값에 1을 더했다. 해당 값의 차를 구하는 것이기 때문에 모든 값에 더해준다면 차는 변하지 않는다. `results` 의 값을 구하기 위해 for loop 를 사용했지만 되도록 지양하고 싶었다. 이 부분은 좀 더 생각을 해봐야겠다.

- toString 을 사용함으로써 코드가 열 댓줄 정도 줄었고, `arr` 부분도 for loop 에서 map 과 filter 를 사용하여 코드를 단순화 시켰다.

- 다른 분들의 풀이를 보니 단 3줄로 끝내버리신 분들도 계셨다. 기계적?프로그래밍적?으로 생각하는 방법이 필요하다고 느꼈다.

```js
function solution(N) {
  // write your code in JavaScript (Node.js 8.9.4)
  const binaryNum = N.toString(2).split("").map(Number);
  const arr = binaryNum.map((el, i) => el && i + 1).filter(Boolean);
  if (binaryNum.every((el) => el) || binaryNum.filter(Boolean).length === 1)
    return 0;
  const results = [];
  for (let i = 0; i < arr.length; i++) {
    if (!arr[i + 1]) break;
    results.push(arr[i + 1] - arr[i]);
  }
  return results.sort((a, b) => b - a)[0] - 1;
}
```
