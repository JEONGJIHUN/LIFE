# Open Chat

## 설명

- [Link](https://programmers.co.kr/learn/courses/30/lessons/42888?language=javascript)

## 풀이

    풀지 못했다. 풀릴 것 같으면서 풀리지 않았다. 접근법부터 잘못되었다. 일차원적으로 들어오는 데이터를 오브젝트로 넣었고, 출력 값도 루프를 돌면서 빈 배열에 넣었다. 그러다보니 이름을 변경할 때 해당 배열을 다시 확인해야하는 상황이 발생했다. 한 시간이 끝나고 어느 부분이 잘못 되었는지 확인해보니 값 출력은 나중으로 미루고 `Map` 을 사용해 입력값과 변경값을 한 번에 처리할 수 있었다. `Map` 을 사용하지 않고 배열쌍으로 사용해도 풀 수 있겠지만 `set` 으로 값을 넣어주고 `get` 으로 해당 데이터의 값을 불러오니 쉽게 처리되었다.

```js
function solution(record) {
  const splitRec = record.map((el) => el.split(" "));
  const mapping = new Map();
  const answer = [];
  splitRec.forEach((el) => el[2] && mapping.set(el[1], el[2]));
  splitRec.forEach(
    (el) =>
      el[0] !== "Change" &&
      a.push(
        `${mapping.get(el[1])}님이 ${
          el[0] === "Enter" ? "들어왔습니다." : "나갔습니다."
        }`
      )
  );
  return answer;
}
```
