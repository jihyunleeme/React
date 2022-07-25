## useState는 왜 let이 아닌 const을 사용할까?

```javascript
  const [const, setCount] = useState(0);
```

값이 변경되면 컴포넌트는 재렌더링된다.
새로운 scope를 생성하고,  
이전 변수와 아무 관련이 없는 새 `count`변수를 생성함.  
재렌더링은 카운트가 `재할당`되지 않음.

- `setCount`를 호출한뒤 컴포넌트는 재렌더링 되고, useState는 는 새로운 값을 return 한다.

```javascript
// 클래스형 컴포넌트
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = { //1️⃣
      count: 0,
    };
  }
}
```

```javascript
// 함수형 컴포넌트
import React, { useState } from "react";

function Example() {
  const [count, setCount] = useState(0); //2️⃣
}
```

- useState는 class 컴포넌트의 `1️⃣`this.state와 동일
- 일반 변수는 함수가 끝날 때 사라지지만, state변수는 React에 의해 사라지지 않음
- useState는 `2️⃣`와 같이 count, setCount를 반환함
- 클래스 컴포넌트의 this.state.count, this.setState와 유사.

### [참고] const의 특징

- block-scoped
- 재할당으로 값이 변경되지 않음
- 재선언 불가
- 값에 대한 read-only 참조로 생성됨
  - 값이 불변성을 유지한다는 의미는 아님
- object, arrary의 property는 업데이트 되거나 제거될수있음

(const - MDN 문서)
[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const]


