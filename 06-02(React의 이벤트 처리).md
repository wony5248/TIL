## React의 이벤트 처리
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
### React의 Event 종류
1. clipBoardEvent : 복사, 잘라내기 등 클립보드에 대한 리스너
  * onCopy
  * onCut
  * onPaste
2. compositionEvent : 이벤트 composition System에 대한 리스너
  * onCompositionStart
  * onCompositionUpdate
  * onCompositionEnd
3. keyEvent : 키보드 입력에 대한 리스너
  * onKeyDown : 키 눌렀을 때에 대한 이벤트, 특수키도 인식한다.
  * onKeyUp
  * onKeyPress : 눌러져 있는동안에 대한 이벤트, 특수키 인식 못한다. (alt, shift...)
4. focusEvent : 해당 DOM요소에 대한 포커스에 대한 리스너
  * onFocus : 해당 요소에 focus가 될 때에 대한 이벤트
  * onBlur : 해당 요소에서 focus가 사라졌을 때에 대한 이벤트
5. formEvent : form 태그의 주요 기능에 대한 리스너
  * onChange
  * onInput
  * onInvalid
  * onReset
  * onSubmit
6. genericEvent : 포괄적인 이벤트에 대한 리스너
  * onError
  * onLoad
7. mouseEvent : 마우스 입력에 대한 리스터
  * Click
    * onMouseDown
    * onMouseUp
    * onClick
    * onDoubleClick
    * onContextMenu
  * Drag
    * onDragStart
    * onDrag
    * onDragEnd
    * onDragExit
  * Hover 
    * onMouseOver : 대상 요소에 마우스가 들어올 때 (자식 element 포함)
    * onMouseMove 
    * onMouseOut : 대상 요소에서 마우스가 벗어날 때 (자식 element 포함)
    * onMouseEnter : 바인딩된 요소에 마우스가 들어올 때 (자식 element 미포함)
    * onMouseLeave : 바인딩된 요소에서 마우스가 벗어날 때 (자식 element 미포함)
  * attribute
  ```
  boolean altKey
  number button
  number buttons
  number clientX
  number clientY
  boolean ctrlKey
  boolean getModifierState(key)
  boolean metaKey
  number pageX
  number pageY
  DOMEventTarget relatedTarget
  number screenX
  number screenY
  boolean shiftKey
  ```
8. pointerEvent : 마우스, 펜, 터치 등 모든 하드웨어의 포인트에 대한 리스너
  * onPointerUp
  * onPointerDown
  * onPointerCancel
  * onPointerOver
  * onPointerMove
  * onPointerOut
  * onPointerEnter
  * onPointerLeave
  * onGotPointerCapture
  * onLostPointerCapture
  * attribute
  ```
  number pointerId
  number width
  number height
  number pressure
  number tangentialPressure
  number tiltX
  number tiltY
  number twist
  string pointerType
  boolean isPrimary
  ```
9. selectionEvent : 텍스트가 선택되었을 때에 대한 리스너
  * onSelect
10. touchEvent : 터치에 대한 리스너
  * onTouchStart
  * onTouchMove
  * onTouchEnd
  * onTouchCancel
11. wheel and scroll Event : 마우스 휠, 스크롤에 대한 리스너
  * onScroll
  * onWheel
12. mediaEvent : 미디어파일에 대한 리스너
  * onAbort
  * onCanPlay
  * onCanPlayThrough
  * onDurationChange
  * onEmptied
  * onEncrypted
  * onEnded
  * onError
  * onLoadedData
  * onLoadedMetadata
  * onLoadStart
  * onPause
  * onPlay
  * onPlaying
  * onProgress
  * onRateChange
  * onSeeked
  * onSeeking
  * onStalled
  * onSuspend
  * onTimeUpdate
  * onVolumeChange
  * onWaiting
13. animationEvent : css 애니메이션에 대한 리스너
  * onAnimationStart
  * onAnimationIteration
  * onAnimationEnd
14. transitionEvent : css 트랜지션에 대한 리스너
  * onTransitionEnd
