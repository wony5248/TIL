# React의 연산자
#### spread 연산자
* 두개 이상의 배열, 객체를 펼칠 수 있는 연산자이다.
* 배열 합치기에서 사용 예시
```
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
이 두배열을 합치기 위해서 기존에는
const arr3 = arr1;
arr3.concat(arr2); 로 해결하던 방식을
const arr3 = [...arr1, ...arr2] => [1, 2, 3, 4, 5, 6] 으로 합쳡진다.
```
* 파라미터에서의 사용 예시
```
const arr1 = [1, 2, 3]
const arr2 = [1, 2, 3, 4, 5]
function sum(x, y, z) {
  return x + y + z;
}
해당 함수에 arr1안의 수들을 인자로 넘겨줄 경우 기존에는 sum(arr1[0], arr1[1], arr1[2]) 이런식으로 넘겨주던 방식을
sum(...arr1) 로 간단하게 이용할 수 있다. 또한 sum(...arr2)를 하더라도 앞에서부터 인자의 갯수인 3개까지만 넘겨진다.
```
* 객체에서의 사용 예시
```
const obj1 = {
  name: 'jbj',
  age: 25
}
const obj2 = {
  phoneNum: 010-4316-3392,
  birth: 1995-04-22
}
const obj3 = {...obj1, ...obj2};
{
  name: 'jbj',
  age: 25
  phoneNum: 010-4316-3392,
  birth: 1995-04-22
}
```
#### rest 문법
* spread연산자와 비슷하게 생겼지만 하는 역할은 완전 다르다.
* rest 문법의 경우 비구조화 할당과 같이 이용된다.
* 객체 에서의 rest
```
const person = {
  name: 'jbj',
  age: 29,
  phone: 010-4316-3392,
}
const {age, ...rest} = person;
age = 29
rest = {name: 'jbj', phone: 010-4316-3392} 가 된다.
```
* 파라미터 에서의 rest
```
함수의 파라미터 갯수가 몇개인지 모르는 경우에 유용하게 이용가능
const function(...rest) {
  return rest.reduce((acc, cur) => acc + cur, 0)
}
function(1, 2, 3, 4)
function(1, 2, 3)
function(1, 2)
인자로 넘겨받은 파라미터로 이루어진 배열이 rest가 된다.
```
#### 삼항 연산자
* if (a === true) return a; 를 삼항 연산자로 표현하면 a === true ? a : undefined 
#### 비구조화 할당
```
const obj {
  name: 'jbj',
  age: 29,
  favorite: 'pizza'
} 
와 같은 객체가 있을 시 해당 객체의 값들을 바로 추출할 수 있는 문법이다.
const [name, age, favorite] = obj; 와 같이 선언해주면 각 값들을 바로 추출하여 이용 가능하다.
```


