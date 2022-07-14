# 2022. 07. 14 TIL

### useNavigate()

```jsx
const **navigate** = useNavigate();

return (
	<button onClick={()=>{
		navigate('/page2')
	}}>
		page2
	</button>
)
```

스크롤을 내리다가 button을 클릭해서 router되는 경우 scroll값이 0,0 이 아닌 채 화면이 보여진다.

라우팅 된 상세페이지의 맨 위 화면을 보여주려면

상세페이지

```jsx
useEffect(()=>{
	window.scrollTo(0,0);
},[])
return (
	//code
)
```

useEffect, 빈배열 (처음 렌더링될 때)

스크롤값을 0,0으로 보내주는 코드를 넣어준다.
