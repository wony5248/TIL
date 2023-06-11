### ES6
* ECMAScript2015, ECMAScript6이라고도 불리며 2015년에 도입된 최신 버전의 JavaScript 이다.
* ECMAScript는 JavaScript 언어가 사용하는 표준으로써, JavaScript 언어가 작동하는 방식에 대한 사양을 제공한다.
* TypeScript의 기반이 되는 클래스 문법과 모듈 기능이 추가 되었다.
* 브라우저에서 지원하지 않는 경우가 있어 Babel이라는 트랜스 파일러를 이용해야 한다.
```
ECMAScript에 포함되는 항목에는 다음과 같은 예가 있습니다.

* 언어 구문 (구문 분석 규칙, 키워드, 흐름 제어, 객체 리터럴 초기화 등)
* 오류 처리 방법 (throw, try...catch, 사용자 정의 Error 유형 등)
* 자료형 (불리언, 숫자, 문자열, 함수, 객체, ...)
* 전역 객체. 브라우저에서 전역 객체는 window 객체지만, ECMAScript는 브라우저에 국한되지 않는 API(parseInt, parseFloat, decodeURI, encodeURI 등)만 정의합니다.
* 프로토타입 기반 상속 구조
* 내장 객체 및 함수 (JSON, Math, Array.prototype 메서드, Object 내성검사 메서드 등)
* 엄격 모드
```
### Babel
* Babel은 JavaScript 컴파일러 이다.
* JavaScript는 컴파일러가 아닌 인터프리터로 동작을 하지만, ES5+ 코드를 브라우저에서 이용가능하도록 하위 버전으로 변환해주는 컴파일러 역할을 한다.
#### Babel이 하는 일
1. Transform syntax(구문 변환)
  * 트랜스 파일링은 최신의 JavaScript 문법을 오래된 브라우저가 이해할 수 있는 오래된 문법으로 변환해준다.
2. babel-polyfill을 통해 polyfill 기능을 지원
  * polyfill은 오래된 브라우저에 native로 지원하지 않는 사용자가 이용하는 메서드, 속성, API가 존재하지 않을 때 추가해 준다.
  * babel은 최신 문법을 오래된 문법으로 변환하는 역할만 할뿐 최신 함수를 이용할 수 있는것은 아니다.
  * babel은 컴파일 때 실행되고, polyfill은 런타임에 실행된다.
3. JSX and React
  * babel은 JSX 문법을 변환한다.
#### Babel의 동작 과정
1. Parsing
  * babel은 소스코드를 분석하여 AST로 변환한다.
2. Transformation
  * 생성된 AST를 브라우저가 지원하는 오래된 문법의 AST로 변경한다.
3. Code generation
  * 새 AST를 바탕으로 새로운 코드를 생성한다.
#### JSX
* JavsScript를 확장한 문법으로 JavaScript + XML로 볼 수 있다.
* JavaScript 내부에서 HTML문법을 사용하는 스펙
##### JSX 문법을 변환해야 하는 이유
* JSX는 JavaScript 코드이지만 브라우저에서 단독으로 실행될 수 없다.
* JSX를 바로 실행하면 브라우저는 이해하지 못하기에 JavsScript(js) 코드로 트랜스 파일링을 해주어야 한다. 
### WebPack
* Webpack이란 한마디로 번들링과 컴파일을 결합하는 '정적 모듈 번들러'이다.
* 여러개로 나눠진 자바스크립트 파일을 html이 실행할 수 있는 하나의 js 파일로 합쳐준다.
#### Webpack의 사용 이유
* 모듈이 많아지게 되면서 자원이 많아지게 되어 관리가 힘들어지는 문제를 해결하기 위해
* 이러한 모든 자원들을 번들링 하기 위해
* 많은 파일을 다운받아야 해서 네트워크 부하가 커지고 느려지는 문제를 해결하기 위해
* 같은 이름의 변수나 함수로 충돌 가능성을 줄이기 위해
#### Webpack의 장단점
* 장점
  1. 성능 최적화 & 자동화
    * 코드 축소와 더불어 사용되지 않는 코드의 제거와 같은 최적화를 통해 웹 사이트 성능 향상시킴
  2. 번들러가 제공하는 편의성
    * Sass나 Stylus등을 이용하거나 typescript 이용 시 번들러가 알아서 필요한 플러그인 추가하여 실행해준다.
  3. codeSpitting을 통한 성능 최적화
    * 필요할 때만 스크립트를 불러오는 lazyLoadint & dynamicLoading이 가능하다.
  4. dependency Issue 해결
* 단점
  1. configuration이 복잡하다 (설정)
  2. 개발 모드 속도가 느리다.
  3. Webpack 번들 크기


