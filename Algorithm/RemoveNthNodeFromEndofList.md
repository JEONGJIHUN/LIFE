# Remove Nth Node From End of List

## 설명

- [Link](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

## 풀이

주어진 linked list 에서 미자막 노드에서부터 n 번째 위치하는 노드를 제거하는 문제이다. 먼저 n 번째 위치한 노드를 구해 loop 를 돌면서 제거해야하는 노드의 위치에 그 다음 노드를 주입하는 방법으로 진행하는 방식이다.

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @param {number} n
 * @return {ListNode}
 */
var removeNthFromEnd = function (head, n) {
  let tem = head;
  while (n) {
    tem = tem.next;
    n--;
  }
  if (!tem) return head.next;
  const result = head;
  while (!!tem.next) {
    head = head.next;
    tem = tem.next;
  }
  head.next = head.next.next;
  return result;
};
```
