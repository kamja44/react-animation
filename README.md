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
