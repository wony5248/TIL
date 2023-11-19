# 할인 행사
```
function solution(want, number, discount) {
    let result = 0
    discount.forEach((v,i)=>{

     let copy=[...discount].slice(i,i+10)
     if(copy.length<10)return result

     let flag=0
     for(let j=0;j<want.length;j++){
      if([...copy].filter(el=>el==want[j]).length==number[j]) 
       flag++

      else break
     }

     if(flag==want.length)result++

  })

    return result
}
discount 배여를 순회하며 10개씩 끊어서 copy배열에 담아준다. 10개 미만일 경우에는 반복문 종료
다음으로 want 배열을 돌며 과일의 갯수가 copy 배열의 갯수랑 같은 경우 flag를 1씩 더해주고, 같지 않을 경우 종료
flag랑 want 배열의 길이가 같을 겨우 result 를 1씩 더해주면 답이 나온다.
```
