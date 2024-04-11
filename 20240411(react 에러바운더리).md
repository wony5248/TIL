# React의 ErrorBoundary 컴포넌트
* ErrorBoundary 컴포넌트는 class로 선언한다.
* 에러를 catch 해주는 컴포넌트이다.
* 이용하고자 하는 컴포넌트를 ErrorBoundary 컴포넌트로 감싸주면 된다.
* 비동기 함수, 서버사이드 렌더링, 에러바운더리 자체에서 발생하는 에러는 잡지 못한다. -> try catch를 이용해 따로 잡아야 함
* 에러가 발생한 이후 화면을 원상복구 하거나 실패한 작업을 재시도 하고 싶을 때에는 react-error-boundary를 이용하는 것이 좋다.
```
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) { // 다음 렌더링에서 폴백 UI가 보이도록 상태를 업데이트 합니다.
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) { // 에러 리포팅 서비스에 에러를 기록할 수도 있습니다. 
    logErrorToMyService(error, errorInfo);
  }

  render() { if (this.state.hasError) { // 폴백 UI를 커스텀하여 렌더링할 수 있습니다.
    return <h1>Something went wrong.</h1>;
  } 
    return this.props.children;
  }
}
```
#### getDerivedStateFormError
* 에러발생 시 state를 변경할 수 있다.
* 에러의 종류에 따라서 분기 처리를 할 수 있다.
#### componentDidCatch
* 에러가 발생할 때 실행되는 라이프 사이클이다.
* 예외를 처리하는 다양한 동작과 state를 바꾸는 것 까지도 처리할 수 있다.
