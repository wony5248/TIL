# 이진변환 반복하기
```
function solution(s) {
  let answer = [0, 0];
  let sLen = 0;

  while (s.length > 1) {
    sLen = s.length;
    s = s.split("0").join("");
    answer[0]++;
    answer[1] += (sLen - s.length);
    s = s.length.toString(2);
  }

  return answer;
}
해설: 문자열의 길이를 저장한뒤 인자로 받는 문자열 s를 0을 제거하면서 반복횟수를 증가시키고, 제거된 0의 개수에 문자열 길이에서 0을 제외한 문자열 길이 뺀값 더해주는것을 반복하면 된다.
```

# 숫자의 표현
```
function solution(n) {
  let answer = 0;
  
  for(let i = 0; i <= n; i++) {
  	if(n%i === 0 && i%2 === 1) answer++;
  }
  
  return answer;
}

해설: 주어진 수를 연속된 숫자의 합으로 표현하는 방법의 수는 주어진 수의 홀수인 약수 갯수가 같다는 공식을 이용하면 된다.
```
