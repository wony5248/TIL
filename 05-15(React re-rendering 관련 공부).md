### React re-rendering 관련 공부
```
* React 의 re-rendering은 아래와 같은 상황에 발생할 수 있다.

부모에서 전달받은 props가 변경될 때
부모 컴포넌트가 re-rendering 될 때
자신의 state가 변경될 때  // setState 함수를 통해 react의 트리거가 업데이트 되는 것
mobx, redux등 중앙 상태값이 변경될 때 // 중앙 상태값이란 컴포넌트의 위치에 상관없이 접근할 수 있는 값
```
* React re-rendering 관련 예제
```
/* 
bad example
React의 상태는 불변성이 유지되어야 하고, 참조값을 업데이트 해주어야지 이전 상태의 일부만을 변경해서는 안된다.
*/
import {useState} from "react";

function App() {
  const [person, setPerson] = useState({
    name: "beomjin",
    age: 29,
    birth: 04/22
  });
  
  function changePerson() {
    person.name = "JBJ";
    setPerson(person);
  } 
```
```
 /*
 good example
 */
 import {useState} from "react";

function App() {
  const [person, setPerson] = useState({
    name: "beomjin",
    age: 29,
    birth: 04/22
  });
  
  function changePerson() {
    setPerson({
      ...person,
      name: "JBJ"
    });
  }
```
```
 /*
 bad example
 해당 예제의 경우 App컴포넌트는 myName의 변화를 알아차리지 못한다.
 */
 function App() {
 let myName;

   function setMyName() {
     myName = "Beomjin"
     setTimeout(() => {
       setMyName();
     }, 1000);
   }
 
   setMyTime();
 
   return (
     <div className="App">
       <Name myName={myName} />
     </div>
   );
 }
 
 function Name(props) {
   return <p>My name is {props.myName.toString()}</p>;
 }
```
```
 /*
 good example
 */
 const [myName, setMyName] = useState("bj");

 useEffect(() => {
   var name = setInterval(() => rename(), 1000);

   return () => clearInterval(name);
 });

 function rename() {
   setMyName("JBJ"); 
 }
``` 
  
* 컴포넌트를 강제로 re-rendering 하는 방법
```
Class 형 컴포넌트의 경우 React에서 제공해주는 forceUpdate() API를 통해 강제로 re-rendering을 시킬 수 있다.
Function형 컴포넌트의 경우 공식 API는 없어서, spread연산자를 통해 새로운 객체로 업데이트 시켜 re-rendering을 시킬 수 있다. (ex. useState를 이용)
```  
* re-rendering 최적화 하는 방법
```
* useMemo 이용하기
  * react Hook중 하나로써 함수들을 캐싱하기 위해 이용
  * 컴포넌트 내부에 함수가 있는 경우 re-rendering이 발생할 때마다 해당 연산을 수행해야 하는 비효율이 있을 경우 useMemo를 이용하면 기존에 함수 반환값을 저장해 놓고 자신이 설정한 변수가 변한 경우에만 해당 연산을 다시 수행한다.
* React.memo 컴포넌트 메모이제이션
  * Hook이 아니기 때문에 Function형, Class형 다 이용 가능
  * React.memo를 이용하면 컴포넌트의 props가 바뀌지 않은 경우 re-rendering을 발생시키지 않도록 해줌
* useCallback
  * useMemo와 마찬가지로 Hook중 하나로써 함수들을 캐싱하기 위해 이용
  * useMemo의 경우 함수의 반환값을 memoize해주는 반면 useCallback은 함수 선언을 memoize하는데 이용
```
