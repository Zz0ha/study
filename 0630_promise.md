# 2022.06.30 TIL

## Promise
``` javascript
let promise = new Promise(function(resolve, reject){
  // executor
})
```
new Promise에 전달되는 함수는 executor (실행함수)이며, executor는 new Promise가 만들어질 때 자동으로 실행되며, 결과를 최종적으로 만들어내는 제작코드를 포함한다.
executor의 인수 resolve와 reject는 Javascript에서 자체 제공하는 콜백이다.
- resolve(value) : 일이 성공적으로 끝난 경우 그 결과를 나타내는 value와 함께 호출
- reject(error) : 에러 발생 시 에러 객체를 나타내는 error와 함께 호출
