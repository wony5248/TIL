# 리액트의 디자인 패턴
1. presentation & container 패턴
  * 컴포넌트 간 의존도가 낮고, presentation 컴포넌트 재사용 가능
  * 컴포넌트 별 역할이 명확하여 코드 구조를 이해하기 쉽다.
  * state를 여러 컴포넌트에 props로 전달하여 상태를 공유할 수 있다.
2. Custom Hooks 패턴
  * 로직을 hooks로 분리하여 관리하는 디자인 패턴이다.
  * 기존의 디자인에서는 다른 Container들에서 공통의 로직 사용할 경우 각각 정의해야 했으나, hooks로 로직을 분리함으로써 로직 재사용이 가능하게 됩니다.
  * 여러 컴포넌트에서 동일한 로직을 공유할 수 있습니다.
  * 컴포넌트의 제어가 쉬워지고 사용자가 더 많은 통제권을 가질 수 있다.
  * 로직이 렌더링과 분리되어 있어 이를 올바르게 연결하려면 컴포넌트의 동작방식에 대한 깊은 이해가 필요하다.
  * 사용 예시
```
    function SearchForm() {

    const { searchKey, onChange, onSubmit } = useSearch();

    return (
        <form onSubmit={onSubmit}>
            <div>
                <label>제목</label>
                <input type="text" value={searchKey} onChange={onChange} name="searchKey"/>
                <button type="submit">검색</button>
            </div>
        </form>
    )
}

export default SearchForm;
```
3. Atomic 패턴
  * 아토믹 디자인은 컴포넌트의 재활용을 최대화 하기 위한 방법론이다.
  * 원자 개념을 사용한 디자인 패턴이다.
  * 작은 컴포넌트가 모여 복잡한 컴포넌트가 되는것이 기본 개념이다.
  * 아토믹 디자인의 구성
    * 원자: UI를 구성하는 가장 작은 요소 ex) 버튼, 아이콘, input, 라디오 버튼 등
    * 분자: 여러개의 원자를 조합하여 형성한 컴포넌트(wotkdydtjd shvdma) ex) 입력 폼, 네비게이션 등
    * 유기체: 분자들이 결합되어 형성된 컴포넌트(재사용성 고려 x) ex) Header, Footer
    * 템플릿: 유기체들이 모여 배치함으로써 페이지 구조나 레이아웃 구성등을 나타냄
    * 페이지: 템플릿에 실제 데이터가 반영된 상태
  * 아토믹 디자인 장점
    * 컴포넌트 사용성 극대화 될 수 있다.
    * 컴포넌트 계층 구조를 알아보기 쉬워 설계 변경이 필요할 시 빠르게 대처 가능
    * 디자인 요소가 재사용될 컴포넌트에 일괄적으로 적용되므로 styles 적용 및 변경이 쉽다.
  * 아토믹 디자인 단점
    * 컴포넌트가 적절하게 분리되지 않으면 컴포넌트 복잡도가 오히려 높아진다.
    * Page부터 Atom까지 너무 많은 props Drilling이 일어나 복잡한 상태관리를 지닌다.
