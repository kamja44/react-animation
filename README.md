# Framer Motion

npm i framer-motion

- import {motion} from "framer-motion"

framer-motion은 일반 HTML태그에 적용할 수 없다.

framer-motion 적용법
<motion.태그명></motion.태그명>
-ex) <motion.div></motion.div>

styled component를 사용하면 framer-motion을 사용할 수 없다.

```js
const Box = styled.div``;
<motion.Box> // Error
```

- framer-motion을 사용하기 위해 다음과 같이 사용한다.

```js
const Box = styled(motion.div)``;
<Box />;
```

## animation props

- motion의 prop으로 작업하기 제일 좋은 것은 animation이다.

### rotateZ

- z축을 설정한 값만큼 회전시킨다.
- animate={{rotateZ: 360}}
  - 요소를 z축을 360도 회전시킨다.

## transition props

- motion의 transition

### delay

- transition={{delay:초}}
  - 지정한 초 후에 animation이 실행된다.

### duration

- trainsition={{duration:초}}
  - 지정한 초 동안 animation이 동작한다.

### type

- animation의 작동방식을 지정할 수 있다.
  - transition={{type:"spring"}}
    - 약간 통통튀는 방식
  - transition={{type:"tween"}}
    - 깔끔하게 끝나는 방식

### stiffness(경직)

- type의 강도를 약한 방향으로 조정할 수 있다.
  - 값이 커질수록 강도가 약해진다.
  - transition={{type: "spring", stiffness : 10}}

### damping(반동)

- type의 강도를 강한 방향으로 조정할 수 있다.
  - 값이 커질수록 강도가 강해진다.
  - 0으로 설정시 계속 반복한다.
  - transition={{type:"spring", damping:10}}

## initial props

- animation의 초기 상태를 지정한다.

### scale

- 요소의 크기를 재정의한다.
- initial={{scale : 0}}
  - 요소의 초기상태의 크기는 0이다.

# variants

- 애니메이션의 stage
  - ex) initial, finish, showing, hidden, from to, 0% 100% 등
  - 즉, 초기상태와 최종상태를 지정한다.

Variants 사용법

```js
// variant 정의
const myVars = {
  start: { scale: 0 }, // 초기 상태
  end: { scale: 1, rotateZ: 360, transition: { duration: 3 } }, // 최종 상태, 최종 상태에서 transition 속성을 지정할 수 있다.
};
function App() {
  return (
    <Wrapper>
      // variaent 적용
      <Box variants={myVars} initial="start" animation="end" />
      // myVars의 start는 initial에 end는 animation에 기술한다.
        <Circle />
        <Circle />
        <Circle />
        <Circle />
      </Box>
    </Wrapper>
  );
}
```

`부모태그가 variants를 갖고 있으면 motion은 자동으로 자식들에게도 variants를 부여한다.`

- 즉, 위의 <Box variants={myVars} initial="start" animation="end" />에서 variants, initial, animation이 자식인 <Circle />에도 부여된다.
  - 자식인 Circle에서도 variants를 사용하기 위해선 부모의 이름과 동일한 이름을 사용해야 한다.
  - 즉, 아래의 코드와 같이 사용해야 한다.

```js
const boxVariants = {
  start: {
    opacity: 0,
    scale: 0.5,
  },
  end: {
    opacity: 1,
    scale: 1,
    transition: {
      type: "spring",
      duration: 0.5,
      bounce: 0.5,
    },
  },
};
const circleVariansts = {
  start: {
    scale: 0,
  },
  end: {
    scale: 2,
    transition: {
      type: "spring",
      bounce: 0.8,
      duration: 5,
    },
  },
};
function App() {
  return (
    <Wrapper>
      <Box variants={boxVariants} initial="start" animate="end">
        <Circle variants={circleVariansts} />
        <Circle variants={circleVariansts} />
        <Circle variants={circleVariansts} />
        <Circle variants={circleVariansts} />
      </Box>
    </Wrapper>
  );
}
```

## Orchestration

- Orchestration의 delayChildren을 이용하여 자식요소들에게 delay시간을 지정할 수 있다.

- Orchestration의 staggerChildren은 각각의 자식요소에 delay를 줄 수 있다.

```js
const boxVariants = {
  start: {
    opacity: 0,
    scale: 0.5,
  },
  end: {
    opacity: 1,
    scale: 1,
    transition: {
      type: "spring",
      duration: 0.5,
      bounce: 0.5,
      delayChildren: 0.5, // 모든 자식요소에 0.5초의 delay를 부여
      staggerChildren: 0.5, // 자식요소 마다 0.5의 추가 딜레이를 부여
      //즉, 첫 번째 Circle은 1초의 딜레이, 두 번째 Circle은 1.5초의 딜레이, 세 번째 Circle은 2초의 delay, 네 번째 Circle은 2.5초의 delay를 갖는다.
    },
  },
};
const circleVariansts = {
  start: {
    opacity: 0,
  },
  end: {
    opacity: 1,
    transition: {},
  },
};
function App() {
  return (
    <Wrapper>
      <Box variants={boxVariants} initial="start" animate="end">
        <Circle variants={circleVariansts} />
        <Circle variants={circleVariansts} />
        <Circle variants={circleVariansts} />
        <Circle variants={circleVariansts} />
      </Box>
    </Wrapper>
  );
}
```

# while

## whileHover

- component에 mousehover 이벤트 발생 시 동작하는 이벤트이다.

```js
<Box whileHover={{ scale: 2 }} />
```

## whileTap

- component 클릭 시(계속 클릭) 이벤트가 발생한다.

```js
<Box whileTap={{borderRadius: "100px"}}>
```

# drag

- component를 드래그할 수 있다.

```js
<Box drag />
```

## whileDrag

- component를 드래그하는 동안 Element를 변경시킬 수 있다.

```js
<Box drag whileDrag={{ backgroundColor: "rgb(46, 204, 113)" }} />
```

# constraint

- component들을 제약한다.

```js
<Box drag="x">
```

- x축으로의 drag만 허용한다.

## dragConstraints

- 드래그의 제약조건을 설정한다.

```js
<Box dragConstraints={{ top: -50, bottom: 50, left: -50, right: 50 }} />
```

# ref

- 코드를 사용해서 특정 Element를 잡을 수 있는 방법

```js
const biggerBoxRef = useRef < HTMLDivElement > null;
<BiggerBox ref={biggerBoxRef}>
  <Box
    drag
    dragConstraints={biggerBoxRef}
    whileDrag="drag"
    variants={boxVariants}
    whileHover="hover"
    whileTap="click"
  />
</BiggerBox>;
```

- ref를 이용하여 레퍼런스를 만들고, BiggerBox에 넣어준다.
- Box에 biggerBox의 가장자리까지 constraints를 넣어준다.

## dragSnapToOrigin

- 기본값 = true
- true인 경우 드래그 가능한 요소는 드래그를 해제할 때, 원점으로 다시 애니메이션된다(원점으로 돌아간다).

## dragElastic

- 외부 제약 조건에서 허용되는 이동 정도이다.
- 0 = 움직임 x, 1 = 전체 움직임
- 기본값은 0.5이다.

# useMotionValue

- component의 값을 추적할 수 있다.

```js
const x = useMotionValue(0);
console.log(x);
return (
  <Wrapper>
    <Box style={{ x: x }} drag="x" dragSnapToOrigin />
  </Wrapper>
);
```

- style의 x좌표가 바뀔 때 마다 MotionValue가 업데이트된다.
- motionValue가 업데이트될 때 React Rendering Cycle을 발생시키지 않는다.

### MotionValue

- state가 아니며, 재랜더링을 발동하지 않는다.

## set

- set 메서드로 업데이트할 수 있다.
- React 리렌더리을 트리거하지 않는다.

## get

- MotionValue는 문자열이나 숫자가 될 수 있다.
- get 메소드를 사용하여 값을 읽을 수 있다.

# useTransform

- useTransform 훅을 사용해서 MotionValues를 연결한다.
- useTransform()는 한 값의 범위에서 다른 값의 범위로 매핑하여 다른 MotionValue의 output을 변환하는 MotionValue를 만든다.

```js
const potato = useTransform(x, [-800, 0, 800], [2, 1, 0.1]);
```

첫 번째 argument

- listening할 component

두 번째 argument

- 검토하길 원하는 입력값들

세 번째 argument

- 얻길 원하는 출력값들

입력값들은 출력값들과 갯수가 같아야 한다.

- 즉, input과 output은 반드시 같은 배열 크기를 가져야 한다.

# useScroll

- 스크롤의 MotionValue를 넘겨준다.

# svg animation

- svg는 path를가지고 있고, path는 fill을 가지고 있다.
- path의 fill 속성을 이용하여 색을 지정할 수 있다.
  - 즉, path의 fill 속성이 svg의 color을 지정한다.
- path의 stroke 속성을 사용하면 윤곽선이 생긴다.
- path의 strokeWidth 속성을 사용하여 윤곽선의 두께를 지정할 수 있다.

```js
<path stroke="white" strokeWidth="2" fill="white" d="..."></path>
```

## pathLength

- 현재 위치까지의 path의 길이를 나타낸다.
- 즉, 윤곽선의 animation을 적용할 때 필요하다

```js
const Svg = styled.svg`
  width: 300px;
  height: 300px;
  path {
    stroke: white;
    stroke-width: 2;
  }
`;
const svg = {
  start: {
    fill: "rgba(255, 255, 255, 0)",
    pathLength: 0,
  },
  end: {
    fill: "rgba(255, 255, 255, 1)",
    pathLength: 1,
    transition: {
      duration: 5,
    },
  },
};

function App() {
  return (
    <Wrapper>
      <Svg
        focusable="false"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 448 512"
      >
        <motion.path
          variants={svg}
          initial="start"
          animate="end"
          d="M224 373.12c-25.24-31.67-40.08-59.43-45-83.18-22.55-88 112.61-88 90.06 0-5.45 24.25-20.29 52-45 83.18zm138.15 73.23c-42.06 18.31-83.67-10.88-119.3-50.47 103.9-130.07 46.11-200-18.85-200-54.92 0-85.16 46.51-73.28 100.5 6.93 29.19 25.23 62.39 54.43 99.5-32.53 36.05-60.55 52.69-85.15 54.92-50 7.43-89.11-41.06-71.3-91.09 15.1-39.16 111.72-231.18 115.87-241.56 15.75-30.07 25.56-57.4 59.38-57.4 32.34 0 43.4 25.94 60.37 59.87 36 70.62 89.35 177.48 114.84 239.09 13.17 33.07-1.37 71.29-37.01 86.64zm47-136.12C280.27 35.93 273.13 32 224 32c-45.52 0-64.87 31.67-84.66 72.79C33.18 317.1 22.89 347.19 22 349.81-3.22 419.14 48.74 480 111.63 480c21.71 0 60.61-6.06 112.37-62.4 58.68 63.78 101.26 62.4 112.37 62.4 62.89.05 114.85-60.86 89.61-130.19.02-3.89-16.82-38.9-16.82-39.58z"
        ></motion.path>
      </Svg>
    </Wrapper>
  );
}
```

## 특정한 property의 transition 시간 정하기

- transition prop

```js
<motion.path
  variants={svg}
  initial="start"
  animate="end"
  transition={{
    default: { duration: 5 },
    fill: { duration: 2, delay: 5 },
  }}
></motion.path>
```

- 모든 property의 default duration을 5로 설정한다.
  - 즉, 모든 property의 duration은 5이다.
- fill property는 duration을 2로, delay를 5로 설정한다.

# AnimatePresence

- React js App 에서 사라지는 component를 animate한다.
- ex) box가 사라질 때의 animation을 적용한다.
- AnimatePresence의 내부에는 조건문이 있어야 하며, component가 visible 상태여야 한다.

```js
<AnimatePresence>
  {showing ? (
    <Box
      variants={boxVariants}
      initial="initial"
      animate="visible"
      exit="leaving"
    />
  ) : null}
</AnimatePresence>
```

- Box의 exit props
  - Box element가 사라질 때 exit에서 설정한 animation을 발생시킨다.

## slider animation

- Box의 position을 absolute로 설정하지 않으면 animation이 깨진다.

```js
import styled from "styled-components";
import { useState } from "react";
import { motion, AnimatePresence } from "framer-motion";

const Wrapper = styled(motion.div)`
  height: 100vh;
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  background: linear-gradient(135deg, rgb(238, 0, 153), rgb(221, 0, 238));
`;
const Box = styled(motion.div)`
  width: 400px;
  height: 200px;
  background-color: rgba(255, 255, 255, 1);
  border-radius: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 27px;
  box-shadow: 0 2px 3px rgba(0, 0, 0, 0.1), 0 10px 20px rgba(0, 0, 0, 0.06);
  position: absolute;
  top: 100px;
`;
const box = {
  invisible: {
    x: 500,
    opacity: 0,
    scale: 0,
  },
  visible: {
    x: 0,
    opacity: 1,
    scale: 1,
  },
  exit: {
    x: -500,
    opacity: 0,
    sacle: 0,
  },
};

function App() {
  const [visible, setVisible] = useState(1);
  const next = () => setVisible((prev) => (prev === 10 ? 10 : prev + 1));
  return (
    <Wrapper>
      <AnimatePresence>
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map((i) =>
          i === visible ? (
            <Box
              variants={box}
              initial="invisible"
              animate="visible"
              exit="exit"
              key={i}
            >
              {i}
            </Box>
          ) : null
        )}
      </AnimatePresence>
      <button onClick={next}>next</button>
    </Wrapper>
  );
}

export default App;
```

## custom

- variants에 데이터를 보낼 수 있게 해주는 property이다.
  - variants에 데이터를 보낼 때 함수를 사용해야 한다.(코드 참조)

## mode="wait"

- exit를 실행시키고 exit이 끝나면 다음 element를 올 수 있게 한다.(코드 참조)

```js
import styled from "styled-components";
import { useState } from "react";
import { motion, AnimatePresence } from "framer-motion";

const Wrapper = styled(motion.div)`
  height: 100vh;
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  background: linear-gradient(135deg, rgb(238, 0, 153), rgb(221, 0, 238));
`;
const Box = styled(motion.div)`
  width: 400px;
  height: 200px;
  background-color: rgba(255, 255, 255, 1);
  border-radius: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 27px;
  box-shadow: 0 2px 3px rgba(0, 0, 0, 0.1), 0 10px 20px rgba(0, 0, 0, 0.06);
  position: absolute;
  top: 100px;
`;
const box = {
  entry: (back: boolean) => ({
    x: back ? -500 : 500,
    opacity: 0,
    scale: 0,
    transition: {
      duration: 0.3,
    },
  }),
  center: {
    x: 0,
    opacity: 1,
    scale: 1,
  },
  exit: (back: boolean) => ({
    x: back ? 500 : -500,
    opacity: 0,
    sacle: 0,
    transition: {
      duration: 0.3,
    },
  }),
};
const ButtonDiv = styled.div`
  display: flex;
  justify-content: center;
  align-items: center;
`;

function App() {
  const [visible, setVisible] = useState(1);
  const [back, setBack] = useState(false);
  const next = () => {
    setBack(false);
    setVisible((prev) => (prev === 10 ? 10 : prev + 1));
  };
  const prev = () => {
    setBack(true);
    setVisible((prev) => (prev === 1 ? 1 : prev - 1));
  };
  return (
    <Wrapper>
      <AnimatePresence custom={back} mode="wait">
        <Box
          custom={back}
          variants={box}
          initial="entry"
          animate="center"
          exit="exit"
          key={visible}
        >
          {visible}
        </Box>
      </AnimatePresence>
      <ButtonDiv>
        <button onClick={prev}>prev</button>
        <button onClick={next}>next</button>
      </ButtonDiv>
    </Wrapper>
  );
}

export default App;
```
