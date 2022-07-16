# 2022.07.13 TIL

## conditional Style

state boolian 값에 따라 스타일을 다르게 설정 하고 싶을 때

ex ) 마우스 스크롤을 올릴 때 navBar를 내리고
스크롤을 내릴 때 navBar를 올린다.

scrollState값이 true면 class명을 ‘navBar down’으로 설정, false면 ‘navBar up’으로 설정

```jsx
const handleScroll = () => {
  setScrollY(window.pageYOffset);
  if (scrollY > lastScroll) {
    setScrollState(false);
  } else if (scrollY < lastScroll) {
    setScrollState(true);
  }
  setLastScroll(scrollY);
};

return (
	<div className={scrollState ? "navBar down" : "navBar up"}></div>
)
```

```css
/* navBar */
.navBar.down {
  position: fixed;
  transform: translateX(0);
  width: 100%;
  height: 104px;
  background: #000;
  color: #fff;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 40px 59px;
  transition: transform 1s;
}
.navBar .navMenu ul {
  display: flex;
  gap: 60px;
}
.navBar.up {
  transform: translateY(-140px);
  transition: transform 1s;
}
```
