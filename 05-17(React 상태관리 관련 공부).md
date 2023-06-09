### React 상태관리 관련 공부
* React의 데이터 흐름
```
React의 경우 부모 -> 자식 단방향으로만 데이터 바인딩이 가능하다.
부모 컴포넌트가 자식 컴포넌트의 상태를 변경하려면 props를 넘겨주어야 변경이 가능 함
부모 - 자식 컴포넌트의 depth가 깊을 경우 props를 계속하여 넘겨주는 것은 구조가 복잡해지고 불필요한 rendering이 증가하게 된다.
이러한 비효율적 요소들을 제어하기 위해 상태관리 라이브러리등을 통해 관리한다.
```
### React의 대표적인 상태관리 라이브러리
* Redux
```
Redux란 javaScript의 상태관리 라이브러리 이다.

    Redux의 세가지 원칙
    1. 동일한 데이터는 항상 스토어(Store)라는 하나뿐인 데이터 공간에서 가지고 와야 한다.
    2. React에서 setState를 통해 상태변경을 하듯이 Redux에서는 action이라는 객체를 통해서만 변경이 가능하다.
    3. 변경은 순수함수(Reducer)로만 가능하다.
    
    Store란?
    Store는 상태과 관리될 수 있는 유일한 공간이다.
    Store에 상태를 저장하고 Store를 통해 상태를 가져온다.
    
    Action이란?
    Action은 Store에 운반할 데이터를 지칭한다.
    Action은 JavaScript의 객체 형식으로 되어있다.
    
    Reducer란?
    Reducer란 이전 상태와 동작을 받아 새 상태를 리턴하는 순수 함수 이다.
    Action을 만들어서 발생시키면 Reducer가 현재 상태와 액션 객체를 파라미터로 받아오고, 새로운 상태를 만들어 반환해준다.
    
    순수함수란?
    동일한 인자가 들어오면 항상 같은 값을 리턴하는 함수
    
    Redux의 장점
    순수 함수를 이용하기에 상태를 예측 가능하다.
    순수 함수를 이용하기에 테스트 하기에 편리하다.
    디버깅이 수월해진다.   
    
    Redux의 단점
    Redux를 이용하게 되면 아주 작은 기능이라도 필수로 만들어야 하는 파일이 있어 코드량이 많아진다.
    러닝커브가 높다.  
```
* context API
```
context API란 React에 내장된 기능으로 props를 이용하지 않고 컴포넌트 간의 값을 공유하도록 해주는 API이다.

    Context란?
    Redux의 store와 같은 역할을 하는 객체
    createContext를 통해 생성하며 Provider와 Consumer를 담고있는 context 객체
    Store와 달리 Context는 여러개를 생성할 수 있다.
    
    Provider란?
    Provider는 state나 action.type에 따른 dispatch 함수들을 valu prop에 넣어서 제공하는 역할을 한다.
    
    Consumer란?
    Consumer는 Provider에 담긴 state와 dispatch 함수들을 필요한 컴포넌트에서 접근할 수 있도록 만드는 역할을 한다.
    
    context APi의 장점
    React에 내장된 라이브러리 이기에 접근성이 좋다.
    다른 상태관리 라이브러리에 비해 러닝커브가 낮다.
    코드구성이 간결한 편이다.
    
    context API의 단점
    context의 provider는 value 값이 변할 경우 값을 사용하는 모든 컴포넌트가 rendering되기에 성능면에서 좋지 않다.
```
* MobX
```
 MobX란 Redux와 마찬가지로 상태관리 라이브러리 이다.
 기본적으로 객체 지향 느낌이 강하다.

    Mobx의 기본 원칙
    MobX는 action이 state를 변경하는 단방향 데이터 흐름을 이용하며, 영향을 받는 모든 View를 업데이트 한다.
    state가 변경되면 모든 derivation이 자동으로 원자단위로 업데이트 된다. -> 중간 값을 관찰할 수 없다.
    모든 derivation은 동기식으로 업데이트 된다.
    computed 값은 느리게 업데이트 된다.
    모든 computed 값은 순수해야 하며 state를 변경해서는 안된다.
    
    Observable란?
    state의 변화를 감시하는 역할을 한다.
    state를 저장하는 추적 가능한 필드라는 것을 의미한다.
    모든 객체, 배열, map과 같은 set은 observable로 설정될 수 있다.
    
    Action이란?
    state를 수정하는 메서드이다.
    
    computed란?
    state의 변화로 인해 계산된 값이다.
    일종의 캐싱값으로 내부에서 사용하는 state가 변경되었을 때만 새로 계산을 하고, 내부 state가 변경되지 않은 경우 기존에 계산해놨던 값을 그대로 사용
    
    Reaction이란?
    observable state를 변경하면 computed가 계산이 되고, computed를 이용하는 곳이 변경되는 것
    computed를 이용하는 컴퓨터를 rendering 하는 것
    
    derivation이란
    state에서 더이상의 상호작용 없이 파생될 수 있는 모든 것
    
    MobX의 장점
    데이터의 흐름과 전파에 초점을 맞춘 패러다임을 따르기에 간단하다.
    주로 Class를 이용하며, 객체 지향적이다.
    불변성을 기본탑재하고 있어 따로 신경쓰지 않아도 된다.
    
    MobX의 단점
    디버깅 툴이 빈약하고, 디버깅이 어렵다.
    레퍼런스 자료가 많지 않고 생태계가 크지 다.
```
