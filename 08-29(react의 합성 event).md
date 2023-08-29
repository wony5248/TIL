## React의 합성 event
### html의 event와의 차이점
* React의 event 이름은 camelCase를 이용한다. ex) onClick
* 문자열이 아닌 함수를 전달한다. ex) onClick = {buttonClick or () => {}}
### 주의해야할 요소
* React에서 event는 DOM 요소에만 설정이 가능하다 ex) div, button, span ...
* 전달해주는 함수의 이름은 handleClick과 같이 handle 접두사를 이용하는 것이 기본적이다.
```
function App() {
  const handleClick = function () {
    alert('hello');
  }
  return (
    <>
      <Component onClick={handleClick} name="장범진" nickname="린밤" />
    </>
  );
}
해당 예시에서 처럼 Component에 넘겨주는 onClick은 event가 처리되지 않고, name, nickname과 같이 props를 전달해주는 것에 불과하다.
```
### React의 함성 이벤트 (Synthetic Event)
* 브라우저 마다 이벤트의 종류, 처리하는 방식이 다르기 때문에 React는 이를 동일하게 처리하기 위해 Synthetic event로 브라우저 마다 다른 native event를 묶어서 처리한다.
* eventHandler는 브라우저에서 이벤트를 동일하게 처리하기 위해 SyntheticEvent 객체를 전달 받는다.
* attribute
```
boolean bubbles : 이벤트가 부모 element로 전파되는지 여부를 반환한다.
boolean cancelable : 이벤트에 규정한 액션을 취소할 수 있는지 여부를 반환한다.
DOMEventTarget currentTarget : 이벤트가 바인딩된 DOM 요소를 반환한다.
boolean defaultPrevented : 해당 DOM의 기본 이벤트가 막혔는지 여부를 반환한다.
number eventPhase : 이벤트의 현재 실행 단계를 반환한다. (0: NONE, 1: CAPTIRING PHASE, 2: AT TARGET, 3: BUBBLING PHASE)
boolean isTrusted : 이벤트가 사용자 행위에 의해 발생됐는지 여부를 반환한다.
DOMEvent nativeEvent : 브라우저 내장 이벤트 객체를 반환한다.
void preventDefault() : 링크나 폼 전송과 같은 기본 동작을 방지하는 메서드
boolean isDefaultPrevented() : preventDefault() 가 호출되었는지 여부를 반환한다.
void stopPropagation() : 부모 element로의 이벤트 전파를 중단하는 메서드 
boolean isPropagationStopped() : stopPropagation이 호출되었는지 여부를 반환한다.
void persist() : v16 까지의 React에서 비동기 콜백함수에서 이용되던 메서드, v17 이후로는 불필요하다.
DOMEventTarget target : 이벤트가 실제로 발생한 요소를 반환한다.
number timeStamp : 이벤트가 발생한 시간을 ms 단위로 반환한다.
string type : 이벤트의 타입을 문자열로 반환한다. (click, erro...)
```
