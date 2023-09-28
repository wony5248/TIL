# React v17 변경 점
####  Automatic Batching
* React-18v 부터 상태 업데이트(setState)를 하나로 통합해서 배치처리를 한 후 리렌더링을 진행합니다.
  * 리렌더링 관련 성능 개선
* 과거 React-17v 에서는 이벤트 핸들러 내부에서 발생하는 상태 업데이트만 배치처리를 지원했습니다.
  * 하지만 이벤트 핸들러 내부에 fetch()등 과 같은 콜백을 받아 처리하는 메소드가 존재할 경우 내부의 콜백이 모두 완료된 후에는 Automatic Batching이 처리되지 않았습니다.
####  Concurrent Feature
* 기존 React에서 추구하고 있는 Concurrent Mode( 동시성 )를 18v 부터 하나의 기능으로 지원하게 되었습니다.
* createRoot
  * 기존 React-17v의 render()와는 다르게 createRoot API를 활용해야 합니다.
  * 동시성 API / Automatic Batching 지원
* startTransition
  * 기존에 사용자 경험을 개선하기위 사용했던 디바운스 / 쓰로틀링 / setTimeout 등의 기능을 지원합니다.
    * 일반적으로 자바스크립트에서 활용하는 setTimeout 동작방식과 다르게 동작합니다.
    * 태스트 큐를 활용하지 않으며 동기적으로 즉시 실행
  * useTransition 훅을 활용하여 isPending 상태값을 가져와 렌더리 결과를 분기 처리 가능
    * isPending: state 변경 직후에도 UI를 리렌더링 하지 않고 UI를 잠시 유지하는 상태
    * 각 상태 업데이트에 대한 우선순위를 설정할 수 있는 Hook 입니다.
  * startTransition만 사용할 수 있습니다.
    * startTransition: 클릭이나 키 입력에 의해 우선순위가 높은 상태 업데이트가 발생할 경우 내부에 선언한 상태 업데이트는 중단되고 클릭이나 키 입력이 끝난 후 이후에 해당 상태 업데이트가 발생합니다.
#### Suspense와 SSR
  * 기존 React SSR 방식은 waterfall 방식을 사용하고 있었습니다.
    * Server는 React 코드를 전달 받음 => HTML로 변환 => React는 다시 변환된 HTML 코드를 전달 받음 => hydrate
    * hydrate: HTML 문서에 자바스크립트를 붙이는 작업
    * 특정 부분에서 병목현상이 발생할 경우 성능 이슈가 발생하게 됩니다.
  * React-18v 는 독립적으로 각각의 렌더링이 가능한 기능이 추가 되었습니다.
    * 기존의 createRoot 대신 hyrateRoot 사용
    * 즉 유저에게 처음 보여주는 페이지 전체를 그려 내려주는 것이 아닌 빠르게 준비되는 부분부터 보여줍니다.
    * HTML Streaming API + Suspense를 연계하여 SSR 설계 지원
    * Selective hydrating 기능 지원
#### HTML Streaming
  * Server에서 HTML 문서를 내려주는 것을 의미합니다.
  * 기존의 React는 renderToString()을 활용하였습니다.
  * 완성된 HTML 문서를 전달 받음
  * React-18v 부터는 pipeToNodeWritable()를 활용해 HTML코드를 작은 청크로 나눈 후 보내줄 수 있습니다.
#### Selective hydrating
  * 상단의 HTML Streaming 기능을 통해 하나의 컴포넌트가 영향을 미치는 빈도수는 감소하였지만 극단적으로 하나의 컴포넌트가 너무 복잡할 경우 계속 <Spinner /> 만 보여지게 됩니다.
  * 즉 다른 컴포넌트들은 렌더링이 완료되고 내려받은 자바스크립트 코드를 hydration 해야하는데 아직 렌더링 되지 않는 컴포넌트 때문에 기다려야 하는 현상이 발생합니다.
  * React-18v 부터는 <Suspense> 를 활용해 구현할 경우 해당 컴포넌트가 아직 렌더링되지 않았어도 상관없이 다른 컴포넌트들은 hydration을 시작할 수 있게 되었습니다.
####  React Server Component(RSC)
  * React에서 node.js와 같은 Server 역할을 수행하는 Server Component 기능을 제공합니다.
    * 브라우저가 받아오는 용량을 줄이기 위해 서버에서 실행되는 컴포넌트입니다.
    * .client.jsx, .server.jsx, .jsx 3개의 파일로 구성
  * 기존 SSR 기능과는 다르게 RSC는 HTML 파일을 가져오지 않고 JSON 데이터를 가져오게 됩니다.
#### New Hooks
  * useId
    * 난수 ID를 생성하는 Hook 입니다.
    * 클라이언트와 서버간의 hydration의 불일치를 피하면서 유니크 아이디를 생성 기능을 제공
    * 특정 key값을 생성하는 것이 아닙니다.
  * useSyncExternalStore
    * 기존의 useMutableSource hook에서 변경되었습니다.
    * 동시성 기능을 사용할 때 전역 상태 관리 라이브러리의 상태가 업데이트 되지 않을 경우 강제로 업데이트를 발생시키는 Hook입니다.
  * useDeferredValue
    * 트리에서 급하지 않은 부분의 재랜더링을 지연할 수 있는 기능을 지원하는 Hook 입니다.
    * 디바운스와 비슷하지만 고정된 지연시간이 없고 렌더링이 반영되는 시점에 지연 렌더링을 시도합니다.
    * 지연된 렌더링은 인터럽트가 가능 => 사용자 입력을 차단하지 않음
  * useInsertionEffect
    * Css-in-JS 라이브러리를 활용할 때 스타일 삽입 성능 문제를 해결할 수 있는 Hook 입니다.
    * Dom이 한번 mutate된 이후 실행되지만 layout effect가 발생하기 전 새 레이아웃을 한번 읽을 수 있기 때문에 사전에 계산할 수 있는 기회가 주어집니다.
    * 기존 useLayoutEffect와 비슷하지만 다른점은 DOM 노드에 대한 참조에 접근할 수 있게 됩니다.
