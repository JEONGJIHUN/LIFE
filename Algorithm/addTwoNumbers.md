# Add Two Numbers

## 설명

- [Link](https://leetcode.com/problems/add-two-numbers/)

## 풀이

linked list 들의 value 값을 역으로 배치시켜 합을 구해 리스트 형식으로 반환하는 문제였다. 기본적으로 제공해주는 ListNode 를 사용하지 않고 list 를 value 값들을 배열로 반환해 합을 구한 뒤 다시 리스트 형식으로 변환해주는 방법을 사용했다.

재귀함수를 사용해 list 와 array 형식으로 변환했다. 테스크케이스를 통과해 제출했지만 리스트의 길이가 길어지니 지금 사용한 방법으로 수가 1E+21 보다 크면 지수표기법으로 결과를 문자열로 반환해 버려 제대로 된 결과값을 얻지 못했다. 하지만 검색 결과 `BigInt` 를 사용해 지수표기법으로 변환되지 않고 큰 정수를 표현하니 통과되었다.

```js
var addTwoNumbers = function (l1, l2) {
  const arr1 = [];
  const arr2 = [];
  const obj1 = {};

  const findValue = (list, arr) => {
    if (!list) return;
    arr.push(list.val);
    while (typeof list.next === "object") {
      return findValue(list.next, arr);
    }
  };
  const reverseJoin = (arr) => arr.reverse().join("");
  const makeList = (arr, obj) => {
    const copiedArr = [...arr];
    if (copiedArr.length === 1) {
      obj.val = copiedArr.shift();
      obj.next = null;
      return;
    }
    obj.val = copiedArr.shift();
    obj.next = {};
    while (copiedArr.length) {
      return makeList(copiedArr, obj.next);
    }
  };

  findValue(l1, arr1);
  findValue(l2, arr2);
  const a1 = reverseJoin(arr1);
  const a2 = reverseJoin(arr2);
  const stringifyAnswer = `${BigInt(a1) + BigInt(a2)}`.split("").reverse();
  const ra = stringifyAnswer.map((el) => Number(el));

  makeList(ra, obj1);
  return obj1;
};
```

하지만 세상엔 많은 사람들이 존재하고 다양한 해답을 가지고 있다. 그 중 인상 깊은 코드를 가져왔다.

```js
var addTwoNumbers = function (l1, l2) {
  function ListNode(val) {
    this.val = val;
    this.next = null;
  }

  let carry = 0;
  const root = new ListNode(null);
  let lastNode = root;

  while (l1 || l2 || carry) {
    let sum = carry;
    if (l1) {
      sum += l1.val;
      l1 = l1.next;
    }
    if (l2) {
      sum += l2.val;
      l2 = l2.next;
    }
    if (sum > 9) {
      carry = 1;
      sum = sum % 10;
    } else {
      carry = 0;
    }
    const node = new ListNode(sum);
    lastNode.next = node;
    lastNode = node;
  }
  return root.next;
};
```
