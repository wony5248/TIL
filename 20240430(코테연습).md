* 연속 부분 수열 합의 개수
```
const solution = (elements) => {
    const sumSet = new Set();
    
    const len = elements.length;
    for (let i=1; i<=len; i++) {
        let sum = 0;
        for (let j=0; j<len; j++) { 
            if (j === 0) {
                for (let k=0; k<i; k++) {
                    sum += elements[k];
                }
            }
            else { 
                sum -= elements[j-1];
                sum += elements[(j+i-1) % len];
            }
            sumSet.add(sum);
        }
    }
    return sumSet.size;
}
슬라이딩 윈도우 알고리즘을 이용하여 부분 수열의 시작부분만 바꿔가며 탐색
set 자료구조를 통해 중복된 값을 제거하면 원하는 결과 도출 가능
```
