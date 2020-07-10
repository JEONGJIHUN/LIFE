# Merge Two Sorted Lists

## 설명

- [Link](https://leetcode.com/problems/merge-two-sorted-lists/)

## 풀이

두 링크드 리스트를 정렬해서 하나의 링크드 리스트를 만드는 문제이다. 링크드 리스트 문제만 접하게 되면 일단 사고가 멈춘다. 풀지 못할 것 같지만 막상 풀이를 보면 쉽게 이해가 간다.. 해결할 수 있다는 생각으로 임해야겠다!

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @retturn {ListNode}
 */
var mergeTwoLists = function (l1, l2) {
  if (!l1 || !l2) return l1 || l2;

  const mergedListeNode = new ListNode();
  let result = mergedListeNode;

  while (l1 && l2) {
    if (l1.val < l2.val) {
      result.next = l1;
      l1 = l1.next;
    } else {
      result.next = l2;
      l2 = l2.next;
    }
    result = result.next;
  }
  result.next = l1 || l2;
  return mergedListeNode.next;
};
```
