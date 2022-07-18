# 2022.07.18 TIL

## 조건에 따라 클릭한 컴포넌트 offset값으로 이동하기
### Home.jsx

```jsx
import { useLocation } from 'react-router-dom';

export default function Home() {
	const { state } = useLocation();
	
	useEffect(()=>{
		const about = document.getElementsByClassName("aboutUsSection")[0].offsetTop;
		const team = document.getElementsByClassName("teamSection")[0].offsetTop;
		const contact = document.getElementsByClassName("contactSection")[0].offsetTop;

		if (state === 'about'){
			window.scroll({top: about})
		} else if (state === 'team'){
			window.scroll({top: team})
		} else if (state === 'contact'){
			window.scroll({top: contact})
		}
	},[state])

	return ( //html코드 )
}

```

### NavBar.jsx

```jsx
import { useNavigate } from 'react-router-dom'

export default function NavBar(){
	const navigate = useNavigate();

	return(
		<div>
			<div onClick={()=>{
				navigate('/', {state: 'about'})
			}}>ABOUT</div>
			<div onClick={()=>{
				navigate('/', {state: 'team'})
			}}>TEAM</div>
			<div onClick={()=>{
				navigate('/', {state: 'contact'})
			}}>CONTACT</div>
		</div>
	)
}
```

1. useNavigate 선언 
const navigate = useNavigate();
2. nav메뉴에서 버튼을 누르면 navigate() 경로 뒤 두번째 인자로 {키, 값} 객체 전달
3. Home.jsx에서 useLocation으로 파라미터를 전달받는다.
4. state라는 변수가 변화될 때마다 리렌더링 하는 useEffect를 만든다.
5. useEffect 안에 각 컴포넌트의 offset값을 담은 변수를 저장한다.
6. 조건문을 사용하여 state가 ‘about’일 때는 scroll이 about 컴포넌트 offset값으로 이동하는 코드,
team일 때는 team컴포넌트로 ….등등 을 짠다.
