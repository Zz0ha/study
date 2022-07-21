# 2022.07.21 TIL

## NodeList, HTML Collection
reference : [https://yung-developer.tistory.com/m/79](https://yung-developer.tistory.com/m/79)

HTML Collection과 NodeList는 모두 유사 배열 객체이면서 이터러블이다. 따라서 둘 다 length 프로퍼티를 가지므로 객체를 배열처럼 접근할 수 있고 반복문을 돌 수 있다. 그러나 유사 배열 객체이기 때문에 자바스크립트에서 제공하는 배열 객체의 메소드는 사용할 수 없다. ex) map, forEach, reduce 등

## getElementsByClassName이나 getElementById 그리고 querySelector의 차이점

getElementByClassName, getElementById는 HTML Collection에 리턴되고,

querySelector, querySelectorAll 은 NodeList에 리턴된다.

### HTML Collection

HTML Collection 객체는 노드 객체의 상태 변화를 실시간으로 반영하는 살아있는 live DOM컬렉션 객체이다. live DOM이기 때문에 객체가 스스로 실시간 노드 객체의 상태 변경을 반영한다.

**예시코드**

```html
<body>
  <div id="app">
    <h1>test</h1>
    <div class="greeting">Hello</div>
  </div>
</body>
```

```jsx

const $app = document.getElementById('app');
const $greeting = document.getElementsByClassName('greeting');
console.log($greeting, $greeting.length); // HTMLCollection [div.greeting] 1
$app.insertAdjacentHTML('beforeend', '<div class="greeting">Hello</div>');
console.log($greeting, $greeting.length); // HTMLCollection(2) [div.greeting, div.greeting] 2

```

HTML코드에서 greeting이라는 class명을 가진 요소는 한개이다. 따라서 첫번째 console.log에서는 길이가 1인 HTML Collection을 출력한다.

이후에 script부분에서 greeting이라는 class명을 가진 요소를 추가시키면 console.log는 길이가 2인 HTML Collection을 출력한다. 

→ HTML Collection이 live객체이기 때문에 요소 노드의 추가나 삭제를 바로 반영시켜준다.

### NodeList

NodeList 객체는 노드 객체의 상태 변화를 반영하지 않는 non-live DOM 컬렉션 객체이다. HTML Collection과 다르게 노드가 변경되어도 그 상태를 반영하지 않는다.

**예시코드**

```html
<body>
  <div id="app">
    <h1>test</h1>
    <div class="greeting">Hello</div>
  </div>
</body>
```

```jsx
const $app = document.getElementById('app');
const $greeting = document.querySelectorAll('.greeting');
console.log($greeting, $greeting.length); // NodeList [div.greeting] 1
$app.insertAdjacentHTML('beforeend', '<div class="greeting">Hello</div>');
console.log($greeting, $greeting.length); // NodeList [div.greeting] 1
```

NodeList객체인 querySelector를 사용하여 변수를 저장했다. script에 HTML을 추가하는 코드를 넣고 console로 찍어보았을 때 이전과 길이가 같은 NodeList를 출력한다. 따라서 NodeList객체는 대부분의 경우 노두 객체의 상태 변경을 실시간으로 반영하지 않고 과거의 정적 상태를 유지하는 non-live객체로 동작한다. 

하지만 childNodes 프로퍼티가 반환하는 NodeList객체는 HTML Collection객체와 같이 실시간으로 노드 객체의 상태 변경을 반영하는 live객체로 동작한다.

**예시코드**

```html
<body id="app">
  <ul id="students">
    <li class="frontend">Gonnie</li>
    <li class="frontend">Poco</li>
  </ul>
</body>
```

```jsx
const $students = document.getElementById("students");
const childNodes = $students.childNodes;

console.log(childNodes instanceof NodeList); //true
console.log(childNodes);
// NodeList(5) [text, li.frontend, li.frontend, text]
// childNodes는 요소노드 뿐만 아니라 공백 텍스트 노드(엔터키)도 포함되어있기 때문에
// NodeList(5) 출력

for (let i=0; i<childNodes.length; i++){
	//removeChild 메서드가 호출될 때마다 NodeList live객체인 childNodes가 실시간으로 변경된다.
	// 따라서 첫 번째, 세 번째, 다섯 번째 요소만 삭제된다.
	$students.removeChild(childNodes[i]);
}

console.log(childNodes);
//NodeList(2) [li.frontend, li.frontend]
```

NodeList는 HTML Collection과 다르게 NodeList.prototype.forEach메서드를 상속받아 사용할 수 있다. 그러나 forEach 외의 Array.prototype에서 제공하는 map, reduce, filter 등의 메서드는 사용할 수 없다.

HTML Collection과 NodeList모두 편하게 사용하기 위해서는 배열로 만들어줘야 한다. HTML Collection과 같은 live객체는 반복문을 순회하면서 노드가 변경되는 경우, 개발자의 의도와는 다른 결과가 발생할 수 있으므로 배열로 바꾸어 사용하는 것이 바람직하다. 
ex) Array.from과 스프레드 연산자 이용

```jsx
const greeting = document.querySelectorAll('.greeting');
Array.from(greeting);
[...greeting]
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b980b953-16f6-42a0-8190-5e071f791809/Untitled.png)
