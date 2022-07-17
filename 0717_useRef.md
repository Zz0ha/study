# 2022.07.17 TIL

## react useRef


Home.jsx

```jsx
import React, { useCallback, useEffect, useRef } from "react";
//eslint-disabled
import Section from "../components/home/Section";
import "../assets/section.css";
import { useLocation } from "react-router-dom";

const Home = () => {
  const { state } = useLocation();

  const mainRef = useRef(null);
  const aboutRef = useRef(null);
  const teamRef = useRef(null);
  const contactRef = useRef(null);

  useEffect(() => {
    switch (state) {
      case "about":
        window.scroll({
          top: aboutRef.current.offsetTop,
          left: 0,
          behavior: "smooth",
        });
        break;
      case "team":
        window.scroll({
          top: teamRef.current.offsetTop,
          left: 0,
          behavior: "smooth",
        });
        break;
      case "contact":
        window.scroll({
          top: contactRef.current.offsetTop,
          left: 0,
          behavior: "smooth",
        });
        break;
      default:
        return false;
    }
  }, [state]);

  return (
    <div>
      <Section ref={mainRef} color="pink" className="section main">
        <h1>Main</h1>
      </Section>
      <Section ref={aboutRef} color="purple" className="section about">
        <h1>About</h1>
      </Section>
      <Section ref={teamRef} color="green" className="section team">
        <h1>Team</h1>
      </Section>
      <Section ref={contactRef} color="blue" className="section contact">
        <h1>Contact</h1>
      </Section>
    </div>
  );
};

export default Home;
```

Section.js

```jsx
import React from "react";

const Section = React.forwardRef((props, ref) => {
  return (
    <div
      className={props.className}
      ref={ref}
      style={{ backgroundColor: props.color }}
    >
      {props.children}
    </div>
  );
});

export default Section;
```
