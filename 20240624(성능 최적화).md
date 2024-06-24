### React 최적화 관련 공부
#### hoos 기반의 성능 최적화 (function component)
* useMemo
```
React에서 CPU 소모가 심한 함수들을 캐싱하기 위해 이용하는 React Hooks
React에서는 어떤 함수의 return 값이 이용되는 컴포넌트 (자식 컴포넌트도 포함)가 re-rendering 될 때마다 함수가 호출이 된다.
useMemo를 이용한다면 종속 변수들이 변하지 않을 시에는 해당 함수를 다시 호출하지 않고 이전 return 값을 재사용 한다.
```
* React.memo
```
React.memo는 hook이 아니기 때문에 클래스형, 함수형 컴포넌트 둘 다에서 이용이 가능하다.
클래스 형 컴포넌트에서 이용가능한 lifeCycleAPI인 shouldComponentUpdate의 대용으로 제시된 API
React.memo를 이용한 컴포넌트의 경우에는 props가 바뀌지 않는다면 re-rendering 되지 않는다.
ex)
//Item.jsx
import React,{ memo } from "react";

function Item({ user }) {
  console.log("Item component render");

  return (
    <div className="item">
      <div>이름: {user.name}</div>
      <div>나이: {user.age}</div>
      <div>점수: {user.score}</div>
      <div>등급: {result.grade}</div>
    </div>
  );
}
export default memo(Item);
```
* useCallback
```
useMemo가 함수의 return되는 값을 memoize 시켜주는 것이라면, useCallback은 함수 선언을 memoize 하는데 이용된다.
함수는 객체이고 새로 생성된 함수는 다른 참조값을 가지기 때문에 다른 props로 인지되어 re-rendering이 일어난다.
```
* useState의 함수형 업데이트
```
useState를 이용할 때 setState를 이용하면서 새로운 상태를 파라미터로 넣는 대신 업데이트 하는 함수를 넣어준다.
ex)
const onRemove = useCallback(
  id => {
    setTodos(todos.filter(todo => todo.id !== id));
  },
  [todos],
);

ex) 함수형 업데이트 후
const onRemove = useCallback(id => {
  setTodos(todos => todos.filter(todo => todo.id !== id));
}, []);
```
* 이벤트 핸들러 제거
```
useEffect 내부에서 addEventListener를 통해 이벤트 등록을 하고 해제해주지 않으면 해당 이벤트가 발생할때마다 계속 이벤트를 감지하기에 성능 저하가 생긴다.
return하는 부분 (unmount 시점)에 removeEventListender를 호출해 제거해주도록 한다.
```
