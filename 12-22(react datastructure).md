# React의 자료 구조
#### Map: 해시 테이블
* Key-value 형태의 자료구조
* 사용 예시
```
const map = {
  name: 'jbj',
  age: 29,
  birth: "1995-04-22"
}
```
#### Set: 중복 제거 배열
* Set은 일종의 배열로 생각하면 된다.
* 중복 원소를 허용하지 않는 배열이다.
* 사용 예시
```
const setArray = [... new Set([1, 2, 2, 3, 3, 3, 4, 4, 4, 4])]  => [1, 2, 3, 4]
```
#### Stack: 이전 작업 추적
* Stack은 선입후출로써 가장 먼저 들어간 원소가 가장 나중에 나온다.
* 가장 위에 원소를 넣을 수 있고, 가장 위 원소를 제거할 수 있다. (push, pop)
* 네이티브 객체는 없으며 배열을 통해 이용 가능하다.
* 이전 작업을 되돌리는 undo 동작에서 주로 사용
* 사용 예시
```
const stack = [];
stack.push(1);
stack.push(2);
stack.push(3);
stack.pop() => 3
```
#### Queue: 순서 보장
* Queue는 선입선출로써 가장 먼저 들어간 원소가 가장 먼저 나온다.
* 네이티브 객체는 없으며 배열을 통해 이용 가능하다.
* 일반적으로 순서를 보장해주는 기능에서 주로 사용
```
const queue = [];
queue.push(1);
queue.push(2);
queue.push(3);
queue.shift() => 1
```
#### Tree: 재귀 구조 데이터
* Tree는 중첩 데이터 구조이다.
* 유사한 자료 구조가 중첩되어 있으며 부모-자식 관계로 보여지며 자식은 또 자식을 가질 수 있다.
* 중첩 메뉴와 같은 컴포넌트에 주로 사용
```
const Family = {
  name: 'grandFather",
  children: [
    {
      name: 'aunt",
    },
    {
      name: 'father",
      children: [
        {
          name: 'brother'
        },
        {
          name: 'me'
        }
      ]
    }
  ]
}
```
#### Array: React의 네이티브 객체
* 배열의 기본 형태로써 배열안에 어떠한 자료형도 넣을 수 있다.
* Array 배열은 참조 타입으로 const로 선언되지만 push를 통해 값을 추가할 수 있다.
* Array method
  * pop: 배열 뒷부분 값 제거
  * push: 배열 뒷부분 값 추가
  * unshift: 배열 앞부분 값 삽입
  * shift: 배열 앞부분 값 제거
  * splice(idx, num, element): 특정 위치(idx)에 요소(element)를 num 개만큼 추가하거나 제거
  * slice:(start, end): 시작 위치(start)에서 종료 위치(end)까지에 대한 shallow copy하는 새로운 배열 객체로 반환
  * concat(arr2): 특정 배열에 다른 배열(arr2)을 합치고 배열의 사본 반환
  * every(fun): 배열의 모든 요소가 제공한 함수(fun)에 부합하는지 테스트
  * some(fun): 배열의 특정 원소가 제공한 함수(fun)에 부합하는지 테스트 - 하나라도 만족하면 true
  * forEach(fun): 배열의 내부를 탐색하면서 해당 원소에 대하여 함수(fun)을 실행
  * map(fun): 배열의 원소별로 함수(fun)을 실행후 결과값을 통해 새로운 배열로 반환
  * filter(fun): 배열을 원소별로 함수(fun)실행 후 만족하는 원소들로만 이루어진 배열 반환
  * reduce(fun): 배열의 각 원소에 대해 더해진 값으로 줄이도록 함수(fun) 적용
  * reverse: 배열의 원소 순서를 거꾸로 바꾼다.
  * sort(fun): 배열을 함수(fun)에 맞는 순서로 정렬한다.
  * toString: 배열을 문자열로 반환한다.
  * valueOf: toString과 같지만 배열형태로 반환한다.
  * join(oper): 배열 전부를 구분자(oper)로 이어진 하나의 문자열로 합친다.


