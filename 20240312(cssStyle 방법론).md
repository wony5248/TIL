### React의 css style
#### css란
* Cascading Style Sheets란 의미로 사용자에게 문서를 표시하는 방법을 지정하는 언어이다.
* 문서란 일반적으로 마크업 언어를 사용하여 구성된 텍스트 파일입니다.
* css는 규칙 기반 언어이다.
#### React에 css style을 적용하는 방법
1. Import 
  * 가장 기본이 되는 방법으로 Component에서 css 파일을 바로 import 하는 방식
  * 가장 간단한 방법이지만, 규모가 커질 경우 관리하기가 어려워진다.
  * classname에도 중복이 발생할 수 있다.
  ```
  import "styles.css";

  const App = () => {
    return(
      <div className="App">
    	...
      </div>
    );
  }
  ```
2. Encapsulation
  * 컴포넌트와 해당 컴포넌트에서 사용하는 css 파일을 묶어서 export 하는 방식
  * Import 방식과의 차이점은 컴포넌트와 사용할 css 파일을 같은 directory 에서 관리한다는 것이다.
  * 코드의 가독성을 떨어트린다는 단점이 있다.
  ```
  import Header from "./Component/Header";

  const App = () => {
    return(
      <div className="App">
    	  <Header />
      </div>
    )
  }

  export default App;
  ```
3. Css Module
  * React에서 제공하는 Css Module
  * css 파일의 확장자를 .module.css로 작성하면 이용이 가능하다.
  * cssModule이 className이 중복되지 않도록 고유하게 이름 부여
  ```
  import styles from "./App.module.css";

  const App = () => {
    return (
      <>
        <div className="App">
          <h1 className={styles.Title}>CSS 적용</h1>
        </div>
      </>
    );
  };

  export default App;
  ```
4. Styled Components
  * css속성을 js 파일 내에서 관리할 수 있는 라이브러리
  * props도 전달이 가능하기에, 조건부 서식 지정도 쉽게 가능하다.
```
import styled from "styled-components";

const StyledHeader = styled.header`
  color: white;
  background-color: black;
  font-size: 20px;
  width: 300px;
  text-align: center;
`;

const Header = () => {
  return <StyledHeader>This is Header.</StyledHeader>;
};

export default Header;
// App.js
import Header from "./Header";

const App = () => {
  return (
    <>
      <div className="App">
        <Header />
      </div>
    </>
  );
};

export default App;
```
5. scss
  * css 전처리기 이다. css Preprocessor라고 불린다.
  * css의 확장으로써 css의 불편함을 상쇄해준다.
  * less, stylus가 가지는 장점을 모두 가진다.
  * 가장 오래된 css 확장 언어이며 높은 성숙도와 커다란 커뮤니티를 갖는다.
  * css 문법과 완전히 호환이 된다.
