---
layout: post
title: "[Vanillacoding] finalTest : Random-chatting-app"
date: 2019-10-05
excerpt: "react, redux, sock-io 등등 배운 원리들을 이용하여 랜덤채팅 만들기"
tag:
- Vanillacoding
- react
- redux
- socket-io
category: [코드리뷰] 
feature: https://kyounghwan01.github.io/lala/assets/img/title/bj_title.jpg
comments: false





---

## 과제명 : Random-chatting-app

> **주요 과제**
>
> 이번 과제는 client는 `react`, `redux` 를 사용하였고, server는 `socket.io` 를 이용하여 실시간 랜덤 채팅을 구현
>
> 1. 로그인 (client : react + redux 사용)
>    1. 랜덤 채팅 취지에 맞게 아무나 이용 가능 하고, 닉네임 입력만으로 접근 가능
>    2. 대기 ui가 보여지고, 매칭시 채팅 시작
> 2. 채팅화면 (서버 : socket.io 사용 )
>    1. `exit` 버튼 누를시 상대방과 나 모두 대화방에서 나감
>       1. server에서 둘다 leave 및 socket.id 삭제
>    2. `next` 버튼 누를시 대기하고 있는 임의의 사람과 연결
>       1. server에서 상대방 room leave
> 3. Test 작성
>    1. client : reducer 함수 기능 테스트
>    2. Component : 렌더링 테스트
>    3. Sever : socket io 서버 테스트 (미완료)



## 이번 과제에서 배운점

### client

## react - Hook

> 기존 class 형 컴포넌트로 우선 개발했다가 함수형으로 전환하면서 hook을 적용함

#### 사용법 

1. `useState` 기존 `setState`를 좀 더 쓰기 용이하게 변경됨

```js
const [error, setError] = useState(null);
//error라는 변수를 사용하고, setError함수로 error를 setState 할것이다.
//null에 들어가는 값은 error의 초기 할당 값

//setState하는 곳에서
setError('에러 발생'); //this.setState({error : '에러발생'}) 과 동일
```

2. `useEffect` 기존 `componentDidMount, componentDidUpdate, componentWillUnmount`를 하나로 묶음

```js
 useEffect(() => {
   //componentDidMount와 componentDidUpdate에 쓸 함수가 오는 자리
    props.connected();
    return () => {
      //이 자리에 오는 함수는 componentWillUnmont와 동일한 작동을 하여 다름 컴포넌트로 				렌더링시 함수 종료됨
      props.connected();
    };
   //[]에 빈 배열이 오는 경우 맨 처음 렌더링만 되고 그 이후 렌더링 되지 않음 			(componentDidMount와 같은 작용)
  }, []);
```

3. componentDidUpdate 사용

```js
useEffect(() => {
   //componentDidMount와 componentDidUpdate에 쓸 함수가 오는 자리
    props.reseiveMessage();
  }, [message]);
//message가 업데이트 될때마다 실행됨
```

4. useRef();

```jsx
const userefExample = props => {
  //ref 정의
 	const userRef = useRef(null);
  return (
    //ref 사용할 곳 정의
    <div ref={userRef}></div>
  )
}
export default userefExample;
```

5. 주의 사항

 useEffect 는 함수를 받는다 async는 함수가 아닌 프로미스를 반환하기에 아래와 같은 경우는 에러를 부른다. 프로미스를 사용할 경우 `usePromise`를 사용한다.

```js
useEffect(async() => {
  //code...
})
//async는 프로미스를 반환하므로 함수만 취급하는 useEffects는 위 코드를 읽을 수 없다.
```



## Redux

> 이번에 사용한 리덕스를 과제를 하면서 내 나름대로 정의

기본적인 파일 구조는

> `action > index.js`, `container > app.js`, `component > 컴포넌트` , `reducers > index.js` 로 구성됨
>
> 데이터의 흐름은 `container` 에서 `dispatch`를 통해 정의된 함수가 `component`에서 실행되면 `action`이 발생하면서 `container`에 정의된 함수가 실행되고 `dispatch`를 통해 `reducers`로 전해지고 `state`가 바뀌면 `store`에 바뀐 `state`가 저장되고 `view`가 리렌더링 된다.



```js
// container/app.js
const mapStateToProps = state => ({
  leaveMessage: state.leaveMessage
  //왼쪽 key 값이 브라우저에 this.props.leaveMessage로 보이는 값
  //오른쪽의 value 값은 reducers에서 combineReducers(아래 코드)를 타고 들어오는 값 
});

const mapDispatchToProps = dispatch => {
  return{
     reseiveMessage() {
      socket.on('receiveMessage', ({ username, message }) => {
        dispatch(receiveMessage(username, message));
      });
    }
  //reseiveMessage로 함수이름이 정의되고 View에서는 reseiveMessage 함수 실행하면 됨
  }
}

// reducers/index.js
export default combineReducers({
  leaveMessage : leaveMessage
  //leaveMessage 이 값은 아래의 코드를 타고 들어오는데
});


export const leaveMessage = (state = initalState.leavemessage, action) => {
  switch (action.type){
    case type.PARTNER_OUT_MESSAGE :
      //action.text는 actions/index.js에서 정의한 값
      return action.text;
    default:
      return state;
  }
}

//actions/index.js
export const partnerOutMessage = (text) => ({
  type: types.PARTNER_OUT_MESSAGE,
  text
});

```



## Scss

> react는 less보다 scss가 더 잘 지원하는 것 같아 사용해봄.
>
> less와 다른 점은 css를 더 잘다루면 느낄 것 같음. 기본적인 사용법은 동일



### server



## socket.io

> 이게 버전이 엄청 자주 바뀌어 검색을 신중히 해야했다.
>
> ^2.3.0을 기준으로 기능 구현함

### 사용법

1. client와 server 연결

```js
io.on('connection', socket => {
  //client와 server 연결 
})
```

2. 서버든 클라이언트든 보내는 쪽은 `emit`, 받는 쪽은 `on` 
   1. sockt은 기본적으로 항상 연결되어있음, 끊겨도 계속 연결하는 모습을 보임
   2. 즉, emit, on은 언제나 어디서나 사용 가능
3. socket에 접속한 모든 클라이언트에게 전송

```js
io.sockets.emit('event', data); //또는
io.emit('event', data);
```

4. 나를 제외한 전체 전송

```js
socket.broadcast.emit('event', data);
//특정 룸에 있는 나를 제외한 모두에게 전송
sockets.to('room id').broadcast.emit('event', data);

```

5. 특정 클라이언트에게 전송

```js
io.to(보낼 socket.id).emit('event' data);

```

6. 특정 room 접속 / 나가기

```js
socket.join(room id); // room 접속
socket.leave(room.id); // room 나가기

```

7. 특정 룸 확인

```js
io.sockets.adapter.rooms['roomNumber']

```

8. emit 과 동시에 param 보내기

```js
socket.to('room id').emit('event', {
      message: '상대방이 나갔습니다',
      text: true
    });

```

8. 룸 및 id 관리 방법

```js
[
  { _id: 'room01', members: ['a_id', 'b_id']},
  { _id: 'room02', members: ['c_id', 'd_id']},
]
// 이렇게 만들되, db에 저장하는게 최적

```

9. 요청 받기

```js
socket.on('event', ({ 받는param1, 받는param2 }) => {
		//이후 받으면 할 행동 함수 or 다른 곳에 emit 
  	//ex)	socket.emit('requestRandomChat');

  	//redux에서는 이곳에서 dispatch 하여 component에게 영향을 줌
	  //ex) dispatch(receiveMessage(username, message));
  });

```

