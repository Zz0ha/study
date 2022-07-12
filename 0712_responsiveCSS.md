# 2022.07.12 TIL

## responsive CSS
### max-**width값 설정**

width값을 % 단위로 설정하고

max-width (width최대값)을 px단위로 설정한다.

500px보다 작은 화면일 때 화면의 50%로 width값이 설정된다.

```css
.section1 {
	width: 50%;
	max-width: 500px;
}
```

### clamp()함수

clamp(min, prefered, max)

prefered : 기본 사용값, 선호하는 값

부모요소를 기준으로 하는 상대 크기, 상대 단위 값을 사용한다. px같은 절대 단위를 사용하면 clamp()함수의 기능을 사용할 수 없다.

상대크기로 가변이지만 min값보다는 작아질 수 없고, max값보다는 커질 수 없다.

```css
.section1 {
	font-size: clamp(1rem, 2.5vw, 2rem)
}
```

→ 2.5vw를 가진 폰트 사이즈를 가지며, 최소 1rem, 그리고 최대 2rem 크기까지 커질 수 있다.

웹 브라우저 너비가 1000px이면 25px 글자 너비가 되고, 보통 웹 브라우저의 기본 글자크기가 16px이므로 최소 16px (1rem)에서 최대 32px (2rem)까지 될 수 있다.

미디어쿼리로 작성한 반응형 웹

```css
.layout {
	font-size : 2rem;
}
@media screen and (max-width:1280px) {
	.layout {
		font-size : 2.5vw
	}
}
@media screen and (max-width:640px) {
	.layout {
		font-size: 1rem;
	}
}
```

위 코드를 **clamp()함수**로 표현

```css
.layout {
	font-size: clamp(1rem, 2.5vw, 2rem)
}
```
