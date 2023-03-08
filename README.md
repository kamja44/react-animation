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
