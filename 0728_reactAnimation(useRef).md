# 2022.07.28 TIL

## react 원하는 element의 offset값에 도달했을 때 애니메이션 구현
스크롤을 내리다가 해당 엘리먼트의 offset에 도달했을 때 해당 Section의 background와 font color를 변경하는 애니메이션을 구상

```jsx
import React, { useRef, useEffect, useState } from 'react'

const ref = useRef(null);
const [blackBackground, setBlackBackground] = useState(false);
const [scrollY, setScrollY] = useState(0);

//scroll에 의한 렌더링
useEffect(() => {
  const handler = () => {
    setScrollY(window.scrollY);
  };
  window.addEventListener("scroll", handler);
  return () => window.removeEventListener("scroll", handler);
}, [scrollY]);

//scrollY값보다 ref로 받아온 document의 offsetTop값이 작으면 state값 변경
useEffect(()=>{
	const rectTop = ref.current.offsetTop;
	if(window.scrollY > rectTop){
		setBlackBackground(true);
	} else {
		setBlackBackground(false);
	}
},[scrollY]);

return (
	<div className={ blackBackground ? "ourValuesSection black" : "ourValuesSection" }>
		{/* 어쩌고저쩌고 코드  */}
		<div ref={ref}>
			<p>여기offset값에 도달하면 배경색이랑 글씨색 바꿔종</p>
		</div>
	</div>
)
```

1. 스크롤이벤트 발생되면 스크롤 값 state (scrollY에 저장)
2. 1.을 useEffect 안에 넣어 scrollY바뀔 때마다 렌더링 유발 (좋은방법인지는 잘 모르겠다)
3. useRef를 사용하여 ref.current.offsetTop값을 rectTop 변수에 저장시킴
4. 내가 구하고자 하는 offset값의 element에 ref={ref} 를 적어준다.
5. 만약 스크롤 Y 값이 rectTop보다 크면 setBlackBackground state를 true로 바꿔주고
6. 그게아니면 setBlackBackground state를 false로 바꿔준다.
7. 그리고 위 내용을 useEffect에 넣어 scrollY값이 변경될 때마다 렌더링하여 값을 비교할 수 있도록 한다.
8. 현재 스크롤값이 rectTop의 offset값보다 크면 blackBackground state가 true로 변경되어 내가 변경하고자 하는 div박스의 class명을 조건문을 통해
blackBackground가 true면 “ourValuesSection black”으로,
false면 “ourValuesSection”의 클래스명을 갖도록 한다.
9. 추가된 클래스명인 (black)의 css를 설정한다.
