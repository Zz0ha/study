# 2022.07.26 TIL

## Spread Operator
스프레드 연산자를 사용하면 배열, 문자열, 객체 등 반복 가능한 객체를 개별 요소로 분리할 수 있다.

```jsx
//Array
var arr1 = [1,2,3,4,5];
var arr2 = [...arr1, 6,7,8,9];

console.log(arr2);
// [1,2,3,4,5,6,7,8,9]

//String
var str1 = 'paper';
var str2 = [...str1];
console.log(str2)
//['p','a','p','e','r'];
```

스프레드 연산자는 연결, 복사 등의 용도로 활용도가 높다.

- 배열에서 Spread Operator

```jsx
var arr1 = [1,2,3];
var arr2 = [4,5,6];

var arr = [...arr1, ...arr2];
console.log(arr)
//[1,2,3,4,5,6]
```

### 함수에서 Spread Operator

- Rest Parameter

함수를 호출할 때 함수의 매개변수(parameter)를 spread operator로 작성한 형태를 Rest parameter라고 부른다. Rest 파라미터를 사용하면 함수의 파라미터로 오는 값들을 모아서 ‘배열’에 집어넣는다.
