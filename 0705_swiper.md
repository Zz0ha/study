swiper 라이브러리 다운로드

```powershell
npm install swiper
```

import

```jsx
import { Swiper, SwiperSlide } from "swiper/react"; // basic
import SwiperCore, { Navigation, Pagination } from "swiper";
import "swiper/css"; //basic
import "swiper/css/navigation";
import "swiper/css/pagination";
```

html코드

```jsx
<Swiper
	direction={"vertical"} //vertical : slider수직방향
	slidesPerView={"auto"} //한 슬라이드에 보여줄 갯수
	mousewheel={true}
	pagination={{
	  clickable: true,
	}}
	modules={[Mousewheel, Pagination]}
	className="mySwiper"
>
	<SwiperSlide className="test1">Slide 1</SwiperSlide>
	<SwiperSlide className="test2">Slide 2</SwiperSlide>
	<SwiperSlide className="test3">Slide 3</SwiperSlide>
	<SwiperSlide className="test4">Slide 4</SwiperSlide>
	<SwiperSlide className="test5">Slide 5</SwiperSlide>
</Swiper>
```

css

```css
#app {
  height: 100%;
}
html,
body {
  position: relative;
  height: 100%;
}

#root {
  height: 100%;
}

body {
  background: #eee;
  font-family: Helvetica Neue, Helvetica, Arial, sans-serif;
  font-size: 14px;
  color: #000;
  margin: 0;
  padding: 0;
}

.swiper {
  width: 100%;
  height: 100%;
}

.swiper-slide {
  text-align: center;
  font-size: 18px;
  background: #fff;

  /* Center slide text vertically */
  display: -webkit-box;
  display: -ms-flexbox;
  display: -webkit-flex;
  display: flex;
  -webkit-box-pack: center;
  -ms-flex-pack: center;
  -webkit-justify-content: center;
  justify-content: center;
  -webkit-box-align: center;
  -ms-flex-align: center;
  -webkit-align-items: center;
  align-items: center;
  height: 100%;
}
.swiper-slide.test1 {
  background: orange;
}
.swiper-slide.test2 {
  background: black;
}
.swiper-slide.test3 {
  background: palevioletred;
}
.swiper-slide.test4 {
  background: palegreen;
}

**/* height값이 100% 가 아닌 section */**
.swiper-slide.test5 {
  **height: 200px;** 
  background: paleturquoise;
}

.swiper-slide img {
  display: block;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

```
