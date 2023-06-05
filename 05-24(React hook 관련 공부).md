### React hook 관련 공부
#### hook의 등장 배경
* class 컴포넌트 vs function 컴포넌트
```
hook이 나오기 전까진 React에서는 state에 대한 접근, lifeCycle 관련 API를 사용하려면 class 형 컴포넌트를 선언해주어야 했다.
function형 컴포넌트는 호출되고 메모리에서 사라지기에 state에 대한 접근, lifeCycle 관련 API 구현이 불가능 했다.
```
* class 컴포넌트의 문제점
```
컴포넌트 간의 로직의 재사용이 불가능 했다.
  * renderProps, HOC(High Order Component)와 같은 패턴으로 해결은 가능하나, 코드의 추적이 어려워짐
  * 코드가 복잡해진다.
이러한 class 컴포넌트의 단점에도 불구하고 state 접근, lifeCycle API 때문에 class 컴포넌트 사용이 불가피 하였다.
```
#### hook의 등장
```
React의 hook은 React 16.8 버전부터 추가된 기능으로 function 컴포넌트에서 state 접근, lifeCycle API를 이용 가능하게 해준다.
React의 hook은 React에서 재공하는 hook과 사용자가 만들수 있는 custom hook이 있다.
```
#### hook의 장점
```
컴포넌트로부터 state 관련 로직을 추상화하는게 가능하다.
계층의 변화 없이 state 관련 로직을 재사용 가능하다.
lifeCycle API를 기반으로 쪼개는 것보다 hook을 통한 작은 함수의 묶음으로 컴포넌트 나누는 방법을 이용 가능하다.
```
#### hook의 규칙
```
최상위 컴포넌트에서만 hook을 호출해야 한다.
  * 반복문, 조건문, 내부 함수에서 hook은 사용이 불가능 하다.
hook을 호출하는 순서는 항상 같아야 한다.
  * hook이 사용된 순서를 보고 react에서는 state 값을 구별한다.
React 함수 컴포넌트 내부에서만 hook을 호출해야 한다.
hook을 만들때 앞에 use 붙히기 (권장)
```
#### hook의 종류
* useState
  * state의 초기값을 정할 수 있고, return 값으로 state와 setState를 반환해주고 state관리를 할 수 있게 해주는 hook이다.
  * const [state, setState] = useState("jbj")와 같은 방식으로 선언할 수 있고 setState("BJ")를 통해 state를 변경이 가능하다.
* useEffect
  * 함수형 컴포넌트에서 이용가능한 lifeCycleAPI를 이용할 수 있게 해주는 hook이다.
  * useEffect는 렌더링 이후 실행할 함수와 observing할 값(배열)을 인자로 받는다.
  * useEffcet의 함수는 rendering할 때 실행되며 내부 return문을 통해 unmount될 때의 동작을 정의할 수 있다.
  * observing할 값을 설정하면 해당 값이 변경될때마다 re-rendering이 일어나게 된다. 설정 안해줄 시 (빈 배열) 최초 렌더링 시에만 실행된다.
```
 useEffect(() => {
    console.log("mount");
    return consoloe.log("unmount");
  }, [count]);
  rendering -> mount 출력
  unmount 시점 -> unmount 출력
  count 값이 변할때마다 rendering
```
* useContext
  * context는 props를 넘겨주지 않고도 트리 전체에서 데이터를 전달할 수 있게 해주는 API이다.
  * useContext를 통해 context에 접근할 수 있다. (consumer와 비슷)
  * context의 변화를 감시하는 역할이다.
* custom hook
  * 주로 input관리 fetch 요청할 때 이용된다.
  * 로직의 반복을 최소화 하고 재사용성 높이기 위해 이용한다.
```
import { useState } from 'react';

const useFetch = (initialUrl: string) => {
  const [url, setUrl] = useState(initialUrl);

  return [url, setUrl];
};

export default useFetch
```



