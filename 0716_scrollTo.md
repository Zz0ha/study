# 2022.07.16 TIL

##버튼 클릭시 scroll값 (0,0)으로 이동


FullPage에서 로고를 클릭했을 때 스크롤값이 0,0으로 이동

```jsx
const [clickLogo, setClickLogo] = useState(false);

useEffect(()=>{
	window.scrollTo(0,0)
},[clickLogo])
// clickLogo의 state값이 변할 때마다 0,0으로 렌더링 하는 useEffect를 만듦

return (
	<div className="logo" onClick={()=>{
		**setClickLogo(!clickLogo)**
		//clickLogo가 true면 false로, false면 true로 변경
	}}>LOGO</div>
)
```

1. logo를 누르면 boolean값이 변경되는 state를 만든다.
2. useEffect로 clickLogo state가 변경될 때마다 렌더링되며, scroll값이 0,0으로 이동하는 함수를 만든다.
3. button을 클릭했을 때 clickLogo state가 false면 true로, true면 false로 변경되는 세터함수를 넣어준다.
4. 버튼을 클릭할 때마다 state값이 바뀌며 렌더링이 된다. (scroll값은 0,0)
