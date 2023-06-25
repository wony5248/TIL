# 프로그래머스 
## 올바른 괄호
```
function solution(s){
    var answer = true;
    let cnt = 0;
    for (let i = 0; i < s.length; i += 1) {
        if (s[i] === '(') {
            cnt += 1
        } else {
            cnt -= 1
        }
        if (cnt < 0) {
            return false;
        }
    }
    if (cnt !== 0) {
        answer = false
    }

    return answer;
}
```
### 해설
```
stack 개념을 이용하여 "("일 경우에 stack에 넣어주고 ")"일 경우에 stack에서 pop 해주면 된다.
또한 다 한 뒤에 stack에 "("가 남아 있을 경우에 대한 처리를 해준다.
중간에 "("가 없는 상태에서 ")"가 들어올 때에 대한 처리를 해주어야 시간초과가 나지 않는다.
```
## 최솟값 만들기
```
function solution(A,B){
    var answer = 0;
    const length = A.length;
    A.sort((a,b) => a - b);
    B.sort((a,b) => b - a);
    for (let i = 0; i < A.length; i += 1) {
        answer += A[i] * B[i]
    }

    return answer;
} 
```
### 해설
```
인자로 받는 A, B 배열에 대해 한 배열의 최댓값과, 한 배열의 최솟값을 곱해주면 된다.
하나는 내림차순, 하나는 오름차순으로 정렬해준뒤 순서대로 곱해주면 된다.
```
