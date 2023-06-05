## React의 이벤트 처리 - 2
### 이벤트의 흐름 3단계
* 캡처링 단계 - 이벤트가 하위 요소로 전파되는 단계
* 타깃 단계 - 이벤트가 실제 타깃 요소에 전달되는 단계
* 버블링 단계 - 이벤트가 상위 요소로 전파되는 단계
### 버블링 
* 한 요소에 이벤트가 발생하면, 이 요소에 할당된 핸들러가 동작하고, 이어서 부모 요소의 핸들러가 동작한다.
* 가장 최상단의 조상 요소를 만날 때까지 이 과정이 반복 되면서 요소 각각에 할당된 핸들러가 동작한다.
* 이러한 흐름을 이벤트 버블링이라고 부른다.
```
<form onClick="alert('form')">FORM
  <div onClick="alert('div')">DIV
    <p onClick="alert('p')">P</p>
  </div>
</form>
1. 해당 예시에서 p태그의 영역을 클릭 시 p에 할당된 onClick 이벤트가 동작
2. 상위 요소인 div 태그의 onClick 이벤트가 동작
3. 최상위 요소인 form 태그의 onClick 이벤트가 동작한다.
```
### event.target과 this의 차이
* event.target은 실제 이벤트가 시작된 target 요소를 가리킨다. 버블링과 상관없이 변하지 않는다.
* this는 현재 요소를 가리킨다. 버블링에 따라 현재 요소는 변한다.
* 위의 예시에서 form의 onClick을 클릭할 경우 event.target과 this는 같지만 p나 div를 클릭하면 다른 요소를 가리킨다.
### 버블링 중단하는 법
1. event.stopPropagation을 이용하면 부모 요소로의 event 버블링을 막는다.
2. event.stopImmediatePropagation을 이용하면 부모 요소로의 버블링에 더불어 요소에 할당된 다른 모든 핸들러의 동작도 막는다.
### 캡처링
* 한 요소에 이벤트가 발생하면 최상위 조상에서 시작해 아래 요소로 전파되는 단계 이다.
* 캡처링 단계에서의 이벤트를 잡아내려면 addEventListner의 capture 옵션을 이용해야 한다.
```
useEffect(() => {
document.getElementById(1).addEventListener("click", () => 캡처링, true)
document.getElementById(2).addEventListener("click", () => 캡처링, true)
document.getElementById(3).addEventListener("click", () => 캡처링, true)

document.getElementById(1).addEventListener("click", () => 버블링)
document.getElementById(2).addEventListener("click", () => 버블링)
document.getElementById(3).addEventListener("click", () => 버블링)
)
<div id={1}>1
  <div id={2}>2
    <div id={3}>3</div>
  </div>
</div>
해당 예시에서 p를 클릭하는 경우
div1 -> div2 -> div3 순서로 캡처링이 일어난다.
div3 -> div2 -> div1 순서로 버블링이 일어난다.
```
### event.evnetPhase
* 해당 프로퍼티를 이용할 경우 이벤트 흐름의 단계를 알 수 있다.
