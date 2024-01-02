# 프레젠테이션 컴포넌트 vs 컨테이너 컴포넌트
#### 프레젠테이셔널 & 컨테이너 디자인 패턴이란?
```
1. 로직을 수행하는 컴포넌트와, markup을 통해 ui를 보여주는 컴포넌트가 분리된 패턴입니다.
2. 그에 따라 앱의 기능과 ui에 대한 구분이 쉬워집니다.
3. 같은 state를 다른 container에게 props 내림으로 상태를 공유 할 수 있습니다.
4. 로직수행, markUp이 다른 컴포넌트에서 하기 때문에 유지보수가 쉽고, 재사용성이 뛰어납니다. 특히, markup 변경에 매우 유연합니다.
5. 동일한 마크업, 컨테이너 레이아웃 (header, footer)는 반복해서 작성하지 않아도 this.props.children 구현 할 수 있습니다.
```
#### 특징
```
1. 컴포넌트 간 의존도가 낮고, presentation 컴포넌트를 재사용 가능하다.
2. 컴포넌트 별 역할이 명확하여 코드 구조를 이해하기 쉽다.
3. state를 여러 컴포넌트에 props로 전달하여 상태를 공유할 수 있다.
```
#### 프레젠테이션 컴포넌트
```
1. 직접적으로 보여지는 부분에 대해 담당한다.
2. Store에 의존적이지 않다.
3. props를 통해 데이터와 callback을 전달 받는다.
4. Markup과 스타일을 가진다.
5. 데이터를 직접적으로 변경하지 않는다.
6. UI 상태값 이외에 대체로 다른 상태값을 가지지 않는다.
```
#### 프레젠테이션 컴포넌트 예제
```
import React from "react";

const Commentlist = comments => (
  <ul>
    {comments.map(({ body, author }) => (
      <li>
        {body}-{author}
      </li>
    ))}
  </ul>
);
props을 기반으로 render 한다.
```
#### 컨테이너 컴포넌트
```
1. 데이터 핸들링에 대한 위주로 개발한다.
2. 마크업이나 스타일을 가지지 않는다.
3. 리덕스의 액션이나 상태 변경에 대한 로직을 담고 있고, 프레젠테이셔널 컴포넌트에 해당 상태를 전달하거나 함수를 제공한다.
4. 다른 프레젠테이셔널 컴포넌트나 컨테이너 컴포넌트를 관리한다.
```
#### 컨테이너 컴포넌트 예제
```
import React from "react";
import CommentList from "./CommentList";

class CommentListContainer extends React.Component {
  constructor() {
    super();
    this.state = { comments: [] };
  }

  componentDidMount() {
    fetch("/my-comments.json")
      .then(res => res.json())
      .then(comments => this.setState({ comments }));
  }

  render() {
    return <CommentList comments={this.state.comments} />;
  }
}
markup 없이 데이터만 다루고 presenter에게 prop으로 전달한다.
```
