# 2022.07.25 TIL

## Intersection Observer API

특정 타겟 엘리먼트가 자기 자신의 조상 엘리먼트들 중 정해진 누군가 또는 최상위 document의 viewport와 교차하는 여부에 변화가 생겼는지 비동기적으로 감지하는 API

```jsx
//npm install react-intersection-observer --save

let observer = new IntersectionObserver(callback, options)
```

1. callback
    - entries : 더 보이거나 덜 보이게 되면서 통과한 역치를 나타내는 IntersectionObserverEntry의 객체 배열
    - observer : 자신을 호출한 IntersectionObserver
2. options
    - root : 교차 기준이 되는 엘리먼트.
    observer의 상위 엘리먼트여야 한다. null이면 viewport가 기준이 된다. (default : null)
    - rootMargin : 교차 기준이 되는 엘리먼트가 가지는 margin값.
    css의 margin속성과 동일하다. (default : 0px 0px 0px 0px)
    - threshold : root엘리먼트와 observer 엘리먼트가 얼만큼 교차되었을 때 이벤트를 실행할지에 대한 옵션. 50% 만큼 보였을 때를 탐지하고 싶다면 0.5로 설정 (default : 0)

```jsx
import { useRef, useEffect, useCallback } from 'react';

const useScrollFadeIn = (direction = "up", duration=1, delay=0) => {
	const element = useRef();
	
	//switch문 사용 케이스 별 애니메이션
	const handleDirection = (name)=>{
		switch(name){
			case 'up' :
				return 'translate3d(0, 50%, 0)';
			case 'down' : 
				return 'translate3d(0, -50%, 0)';
			case 'left' :
				return 'translate3d(50%, 0, 0)';
			case 'right':
				return 'translate3d(-50%, 0, 0)';
			default:
				return;
		}
	}	

	const onScroll = useCallback(
		([entry])=>{
			const { current } = element;
			if (entry.isIntersecting){
				current.style.transitionProperty = 'all';
				current.style.transitionDuration = `${duration}s`;
				current.style.transitionTimingFunction = 'cubic-bezier(0,0,0.2,1)';
				current.style.opacity = 1;
				current.style.transform = 'translate3d(0,0,0)';
			}
		},
		[delay, duration],
	);

	useEffect(()=>{
		let observer;
		
		if(element.current){
			observer = new IntersectionObserver(onScroll, {threshold: 0.7});
																				//콜백함수, {옵션}
			observer.observe(element.current);
		}
		return ()=> observer && observer.disconnect();
	},[onScroll]);
	
	return {
		ref: element,
		style: {opacity: 0, transform: handleDirection(direction)},
	};
};

export default useScrollFadeIn;
```

```html
<ItemBox {useScrollFadeIn('up', 1, 0)}>
  <div>what</div>
</ItemBox>
```
