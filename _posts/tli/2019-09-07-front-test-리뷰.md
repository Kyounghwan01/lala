---
layout: post
title: "[과제정리] frontTest : 채팅 어플리케이션"
date: 2019-09-07
excerpt: "react, react-router, redux 과제 리뷰"
tag:
- Vanillacoding
- react
- react-router
- redux
- jest
- enzyme
category: [코드리뷰] 
feature: https://kyounghwan01.github.io/lala/assets/img/title/bj_title.jpg
comments: false





---

## 채팅 어플리케이션

> **주요 과제**
>
> react, react-router, redux 이용하여 채팅 어플리케이션 만들기 <br>(front만 만들기에 server는 mockup data 사용, 이후 firebase 연동)


## react

> 적용한 원리가 너무 많아 내가 고민하고 해결했던 것만 기술 (doc에 있지만..)

1. `this.setState()` 콜백

> `setState`는 좀 느리다. 그래서 비동기로 할 때 애먹는 일이 있다.
>
> 예를 들어 state에 오름차순으로 정렬, 내림차순으로 정렬이 있다 할때, 버튼을 눌러 setState를 한다해도 state 자체는 변경이 되지만 느리게 되어 render되는 화면은 state가 변경되지 않게 보일 때가 있다.
>
> 그럴때 `setState` 의 callback 함수를 이용하면 된다.

```javascript
this.setState({ howToSort: 'asc' })
//이렇게 정의하면 asc, 오름차순으로 정렬 state가 바뀌기는 하나 render가 원하는 방향으로 되지 않는다. 그래서
this.setState({ howToSort: 'asc' }, () => {
  reRender();
  //code ...
});
//이렇게 콜백을 이용하면 원하는 결과를 얻을 수 있다.
```

2. `componentWillUnmount` 의 중요성

> 어플리케이션이 작을 때는 상관이 없지만 component가 늘어나고 기능이 많아지면 `componentWillUnmount` 로 삭제해주는 작업은 꽤 중요하다.
>
> 예를 들면 스크롤 감지에 대한 내용이다. 

```javascript
export default class App extends Component {
  componentDidMount(){
    window.addEventListener('scroll', scrollFunc);
  }
  //scroll할때마다 scrollFunc이 실행됨
  //만약 이 함수를 삭제하지 않고 다른 컴포넌트로 이동하면 그 컴포넌트도 계속 함수가 실행되고있다. 그러므로 componentWillUnmount를 하여 기능을 중지 해야한다.
  componentWillUnmount(){
    window.removeEventListener('scroll', scrollFunc);
  }
}

//그런데, react hook을 쓰면 더 간단하게 컴포넌트 관리가 가능하다.

useEffect(() => {
  //추가
  window.addEventListener('scroll', scrollFunc);
    return () => {
      	//삭제
        window.addEventListener('scroll', scrollFunc);
    };
  }, []);
```

3. data를 불러오는 `fetch`, `axios`의 경우 `async/await`를 활용하면 보기 쉬운 코드로 만들 수 있다.

```javascript
return fetch(`/api/v1/articles...`).then(res => res.json())
        .then(data => {
          this.setState({ listData: data.posts });
        });
//이렇게 fetch 해서 json으로 바꾸고 setState하는 작업을 async await으로 하면
const fetchData = await fetch(`/api/v1/articles....`);
const fetchDataJson = await fetchData.json();
this.setState({listData: fetchDataJson.posts});

//이렇게 보기 쉬운 코드로 만들 수 있다.
```

4. 왠만한 것들은 map 함수로 가능하니 구현할 때 생각좀 많이 하고 짰으면 한다 (foreach, for문 2번 돌리지 말고...)
5. CORS

> cors는 다른 도메인에서 자료를 요청하면 거부하는 것으로 여러가지 해결방법이 있다.<br>

1. react webpack 내부에 proxy를 허용시키는 방법 (비추)
2. 직접 서버를 만들어 우회하는 방법 (서버와 서버간의 ajax통신은 cors를 만들지 않는다) 
   즉, client가 내가 만든 server로 요청 ( 이때, 내가 만든 서버의 cors에 내 클라이언트 ip를 whitelist만들어 허용한다 ) <br>내가 만든 server에서 원하는 자료가 있는 client로 api 요청하면 cors문제가 걸리지 않는다.
3. prop-types

> 컴포넌트의 prop이 어떤 자료형태인지 기술한다 (오류 방지)

```javascript
import PropTypes from "prop-types";

Chat.propTypes = {
  onLoad: PropTypes.func,
  chats: PropTypes.array
};

```




## redux

> Reduce + flux 
>
> reduce는 보통 아는 그 reduce 함수로 initstate가 있으면 accumulator 에 의해 state가 더해지는 형식이다.<br>flux 패턴은 단방향으로 이어지는 데이터 흐름을 말하며 view 단에서 액션을 발생하면 액션은 store에서 state를 가져오고 dispatch를 통해 reducer에 정의된 흐름에 따라 state가 변화하고 다시 store에 저장되는 패턴
>
> redux를 구현하고 실행하는 것은 finaltest 리뷰에서 다루겠다.

react hook에서 `useReduce`를 이용하면 더 쉽게 state를 관리 할 수 있다.

#### Side effect

redux를 통해 state를 관리하던 중 api호출하거나, 데이터를 db에 저장하거나 다른 행위를 할 경우를 `side effect`라고 부르는데 이것을 관리하기위해 `react-saga`가 있다고 한다. 사용해보지 않아서 어떻게 뭐가 좋은지는 잘 모르겠다. 

#### redux test

나는 jest를 이용하여 테스트를 하였다 

1. initstate가 제대로 들어가는지
2. reducer 함수를 통해 action이 발생 했을때, initstate가 원하는 state로 변경이 되었는지
