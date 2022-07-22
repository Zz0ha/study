# 2022.07.22 TIL

## LifeCycle, useEffect

- Mount - 생성 (컴포넌트가 처음 나타났을 때)
- Update - 재렌더링 (특정 props가 바뀔 때)
- Unmount - 삭제 (사라질 때)

클래스 컴포넌트에서 lifecycle hook사용

```jsx
class Detail2 extends React.Component {
	componentDidMount(){
		//Detail2 컴포넌트가 로드되고나서 실행할 코드
	}
	componentDidUpdate(){
		//Detail2 컴포넌트가 업데이트 되고나서 실행할 코드
	}
	componentWillUnmount(){
		//Detail2 컴포넌트가 삭제되기 전에 실행할 코드
	}
}
```

→ 요즘은 useEffect로 Lifecycle hook을 사용한다

useEffect사용해서 console.log가 두번 출력되는 건 index.js에 <React.StricMode>라는 태그가 있기 때문에 두번 출력됨 디버깅용으로 편하라고 사용됨

useEffect안에 적은 코드는 html렌더링 이후에 동작함

**예시코드**

```jsx
function Detail(){
	//(반복문 10억번 돌리는 코드)

	return (
		<div></div>
	)
}
```

이렇게 코드를 짜면 반복문 다 돌리고 나서 하단의 html을 보여줌

```jsx
function Detail(){
	useEffect(()=>{
		//반복문 10억번 돌리는 코드
	});

	return (
		<div></div>
	)
}
```

이렇게 코드를 짜면 html을 보여주고 나서 반복문을 돌림
오래걸리는 반복연산, 서버에서 데이터 가져오는 작업, 타이머 등등 html렌더링 같은 핵심기능 이외의 기능들을 useEffect안에 적는것이 좋다.

### useEffect clean up function

useEffect 동작하기 전에 특정 코드를 실행하고 싶을 때 return ()⇒{} 안에 넣을 수 있다.

```jsx
useEffect(()=>{
	//그 다음 실행되는 코드
	return ()=>{
		//여기있는 코드가 먼저 실행됨
	}
},[])
```

clean up function을 사용하는 이유 :
setTimeout()을 쓸 때마다 브라우저 안에 타이머가 생긴다. useEffect안에 썼기 때문에 컴포넌트가 mount될 때마다 실행된다. 그러면 타이머가 마운트 될 때마다 계속 생기게됨
그를 방지하기 위해 useEffect에서 타이머 만들기 전에 기존 타이머를 제거하는 함수를 만들어줄 때 사용한다.

```jsx
useEffect(()=>{
	let a = setTimeout(()=>{ setAlert(false) },2000)
	return ()=>{
		clearTimeout(a)
	}
},[])
```

- clean up function에는 타이머 제거, socket 연결요청제거, ajax요청 중단 같은 코드를 많이 작성함
- 컴포넌트 unmount시에도 clean up function 안에 있던게 1회 실행됨

### useEffect 정리

```jsx
//재렌더링마다 코드 실행 가능
useEffect(()=>{ 
	//실행코드
})

//컴포넌트 mount시 1회만 실행 가능
useEffect(()=>{ 
	//실행할 코드
 },[])

//useEffect안의 코드 실행 전에 항상 실행
useEffect(()=>{
	return ()=>{
		//실행할 코드
	}	
})

//컴포넌트 unmount시 1회 실행
useEffect(()=>{
	return ()=>{
		//실행할 코드
	}
},[])

//state1이 변경될 때만 실행
useEffect(()=>{
	//실행할 코드
},[state1])
```
