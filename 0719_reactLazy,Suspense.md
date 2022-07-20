# 2022.07.19 TIL

## React lazy, suspense

App.js

```jsx
import { lazy, Suspense, useEffect, useState } from "react";
import { BrowserRouter as Router, Routes, Route } from "react-router-dom";
import "./App.css";
import Loading from "./components/Loading";
const Home = lazy(() => import("./components/Home"));
const NavBar = lazy(() => import("./components/NavBar"));
const Detail = lazy(() => import("./pages/Detail"));
// import Home from "./components/Home";
// import NavBar from "./components/NavBar";
// import Detail from "./pages/Detail";

function App() {
  return (
    <Router>
      <Suspense fallback={<Loading />}>
        <NavBar />
        <Routes>
          <Route path="/" element={<Home />}></Route>
          <Route path="/detail" element={<Detail />}></Route>
        </Routes>
      </Suspense>
    </Router>
  );
}

export default App;
```

lazy함수를 사용하면 동적 import를 사용해서 컴포넌트 렌더링 가능

lazy, Suspense import해주기.

lazy컴포넌트는 Suspense컴포넌트 하위에서 렌더링 되어야함.

Suspense는 lazy컴포넌트가 로드되길 기다리는동안 로딩화면같은 예비 컨텐츠를 보여줄 수 있음 → fallback prop은 컴포넌트가 로드될 때까지 기다리는 동안 렌더링 하려는 react엘리먼트를 받아들임
