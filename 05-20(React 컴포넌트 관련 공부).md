### React 컴포넌트 관련 공부
* React 는 함수형 컴포넌트와 클래스형 컴포넌트를 이용하여 컴포넌트를 선언할 수 있다.
* 클래스형은 이전에 주로 이용되었고, 현재는 함수형 컴포넌트가 더 많이 이용되는 추세이다.

### 클래스형 컴포넌트와 함수형 컴포넌트의 차이
* 함수형 컴포넌트의 선언 방식
```
import React from 'react';
import './App.css';

function App() {
  const name = 'react';
  return <div className = "react">{name}</div>
}

export default App;
```
* 클래스형 컴포넌트의 선언 방식
```
import React, {Component} from 'react';

class App extends Component {
  render() {
    const name = 'react';
    return <div className="react">{name}</div>
  }
}

export default App;
```
* lifeCycle 관점에서의 차이
```
              클래스형                          함수형
Mounting    constructor()                함수형 컴포넌트 내부
Mounting    render()                      return()
Mounting    componenDidMount()            useEffect()
Updating    componentDidUpdate()          useEffect()
UnMounting  componentWillUnmount()        useEffect()
클래스형 컴포넌트는 lifyCycleApi의 사용이 가능하다 
함수형 컴포넌트는 hook을 통해 lifeCycle 관련 기능 사용이 가능하다.

클래스형의 경우 함수형 컴포넌트에 비해 메모리 자원이 더 이용된다.
```
* state 이용관점에서의 차이
```
클래스형 컴포넌트에서는 state 값을 설정할 수 있고, this.setState를 통해 state의 값을 변경할 수 있다.
함수형 컴포넌트에서는 useState 함수를 통해 state를 설정하고 변경할 수 있다.
```
* props 이용관점에서의 차이
```
클래스형 컴포넌트의 경우 this.props를 통해 넘겨받은 props 값을 불러올 수 있다.
함수형 컴포넌트의 경우 props를 전달받으면 불러올 필요 없이 호출이 가능하다.
```
* 이벤트 핸들링 관점에서의 차이
```
클래스형 컴포넌트에서는 애로우 펑션을 이용해 바로 선언이 가능하고 요소에 this를 붙여서 적용이 가능하다.
함수형 컴포넌트에서는 const 키워드 + 함수 형태로 선언을 해야하며 요소에 this 없이 적용이 가능하다.
```
