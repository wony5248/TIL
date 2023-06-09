## Javascript의 이벤트 루프
### JavaScript 엔진
* javaScript의 엔진은 크게 2개로 콜스택 영역과, 힙 영역이 있다.
* javascript 엔진은 단순히 태스크가 요청되면 콜 스택을 통해 요청된 작업을 순차적으로 실행한다.
### 이벤트 루프
콜 스택에 현재 실행중인 실행 컨텍스트가 있는지 반복해서 확인한다.
만약 콜스택이 비어있고, 태스크 큐에 대기중인 함수가 있다면 이벤트 루프는 FIFO로 태스크 큐에 대기중인 함수를 콜 스택으로 이동 시킨다.
```
function foo(b) {
  let a = 10
  return a + b + 11
}

function bar(x) {
  let y = 3
  return foo(x * y)
}

const baz = bar(7) // 42를 baz에 할당
```
#### 콜스택
* 함수를 호출하면 함수 실행 컨텍스트가 순차적으로 콜스택에 푸쉬되어 순차적으로 실행된다.
* Javascript의 경우 하나의 콜 스택을 이용하기 때문에 최상위 실행 컨텍스트가 콜스택에서 제거되기 전까지는 어떤 태스크도 실행되지 않는다.
#### 힙
* 힙은 객체가 저장되는 메모리 공간이다.
* 메모리에 값을 저장하려면 메모리 공간의 크기를 결정해야 한다.
* 힙은 구조화 되어 있지 않다는 특징이 있다.\
#### 태스크 큐
* 브라우저에서 제공해준다.
* setTimeout, setInterval과 같은 비동기 함수의 콜백 함수 또는 이벤트 핸들러가 보관되는 영역

위 코드의 실행 순서는 
1. bar를 호출할 때 bar의 인수와 지역 변수 포함하는 첫 번째 프레임 생성
2. bar가 foo를 호출할 때 foo의 인수와 지역변서 포함하는 두번째 프레임 생성되어 첫번째 프레임 위로 push 됨
3. foo가 반환하면 맨위의 프레임 요서 pop
4. bar가 반환되면 스택이 비게된다.

### macroTaskQueue 와 microTaskQueue
* 태스크 큐의 종류이다.
#### microTask
* 일반 이벤트 실행문이 아닌 특정 코드를 사용해서만 만들 수 있고, 주로 promise를 통해 만든다.
* 사용한 함수나 프로그램이 종료된 후 콜스택이 비어져있을 때 실행되는 짧은 함수
#### macroTask
* 이벤트 루프의 stack이나 microTaskQueue가 비어져 있을 때 실행되는 짧은 함수
* setTimeout, setInterval, setImmediate등이 있다.
#### 호출 순서
1. 매크로태스크 큐에서 가장 오래된 태스크를 꺼내 실행한다.(예: 스크립트를 실행)
2. 모든 마이크로태스크를 실행한다.이 작업은 마이크로태스크 큐가 빌 때까지 진행되며, 태스크는 오래된 순서대로 처리된다.
3. 렌더링할 것이 있으면 처리합니다.
4. 매크로태스크 큐가 비어있으면 새로운 매크로태스크가 나타날 때까지 기다린다.
5. 1번으로 돌아간다.
