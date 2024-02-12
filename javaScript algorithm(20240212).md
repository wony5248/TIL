# JS의 문법
### 연산
#### AND OR
* and: &&
* or: ||
#### 증감 연산자
* ++: 대입 후 더해줌
* --: 대입 후 빼줌
#### for 문
* 기본 for문
```
for(let i = 0; i < 100; i += 1){
  return i // 1 ..... 100
}
```
* forEach
```
const arr = [1, 2, 3, 4, 5];
arr.forEach((child) => {
  console.log(child) //1, 2, 3, 4, 5
})
map 문법과 유사하지만, map 과는 다르게 return이 없다.
```
* for value in array
```
const array = [1, 2, 3];
for (let value of array) {
  console.log(value); // 1, 2, 3
}
```
#### 배열 연산
* unshift: 배열의 맨 앞에 값 추가
* push: 배열의 맨 뒤에 값 추가
* find: 특정 값을 찾아준다.
* sort((a,b) => a - b): 오름차순 정렬
* sort((a,b) => b - a): 내림차순 정렬
* arr.join(","): ,를 기준으로 배열 값들을 이어 붙여 문자열로 반환
#### 집합 연산
* 선언
```
const Set = new Set([1, 2, 3, 4, 5])
```
* 합집합
```
const set = new Set([...setA, ...setB])
```
* 교집합
```
const intersection = new Set([...setA].filter(x => setB.has(x)))
```
* 차집합
```
const difference1 = new Set([...setA].filter(x => !setB.has(x))); // set1 - set2
const difference2 = new Set([...setB].filter(x => !setA.has(x))); // set2 - set1
const symmetricDifference = new Set([...difference1, ...difference2]); // union - intersection
```
* 집합을 배열로
```
Array.from(tmp).sort((a, b)=>b-a);
```
#### 문자열
* length: 문자열의 길이
* strint[n]: n번째 문자
* indexOf(n): n이 시작되는 문자열 index 반환 -1일경우 문자열에 없는 문자이다.
* slice(s, e): s 부터 e-1 까지의 문자 반환 (불변성 유지)
* toLower, toUpper: 소문자, 대문자로 변환된 값 리턴
* replace('a', 'b'): a 문자을 b로 바꾼 문자열 리턴
* split(','): ,로 나누어진 문자를 배열로 변환하여 리턴
