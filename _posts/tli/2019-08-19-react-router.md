---
layout: post
title: "[코드리뷰] react-router"
date: 2019-08-19
excerpt: "6주차 과제 코드리뷰"
tag:
- 코드리뷰
category: [코드리뷰]
feature: https://kyounghwan01.github.io/lala/assets/img/title/bj_title.jpg
comments: false



---



### 1. exact 정확히 파악

> 주어진 경로와 정확히 맞아야만 컴포넌트를 보여준다.

```jsx
// http://localhost:3000 에서만 Home를 보여준다.

<div>
  <Route exact path="/" component={Home}/>
  <Route path="/about" component={About}/>
</div>

//exact가 없을 경우 
//http://localhost:3000/about에 들어가면, Home 컴포넌트와 About 컴포넌트 둘다 보여짐 (/about에도 '/' 가 있기 때문)
```



### 2.  변동되는 부분은 상수로 관리

- 각 역할에 따라 디렉토리 분리할 것



### 3. this.setState는 promise를 반환하지 않기에 await 불가

> setState는 비동기로 작동하기에 즉시 컴포넌트를 업데이트 하지 않는다.
>
> 그렇기에 원하는 결과를 얻으려면 componentDidUpdate나 setState 콜백을 사용해야한다.

```js
//잘못된 async await 사용
ascBtn = async () => {
  await this.setState({
    //code ...
  })
}
```

```js
//setState의 콜백 활용
ascBtn = () => {
      this.setState({ listData: [], howToSort: 'asc' }, () => {
        try {
          this.fetchInitPage().then(this.renderPost());
        } catch {
          alert('데이터 패치 오류입니다 관리자에게 문의하세요');
    });
```



### 4.  네이밍..... (고질적인 문제군요)

```jsx
 if (!page) {
      return;
    } else {
// code ...
    }
```



### 5. window.reload()는 api call을 다시 부르니 `setState`를 통해 re-render되는 방법으로 생각하도록



### 6. 전체적으로 state에 담는 정보를 조금 더 깊이 생각하고 구성했으면 좋겠습니다. 그때 그때 필요하다고 생각해서 약간 즉흥적으로 넣은 것 같은 느낌이 있는데, 스테이트 내부에 중복되는 자료도 많고 이름도 불분명한 것들이 많네요.

- 앱을 만들때 전체적인 데이터 구조를 짜고 시작하는 것이 맞을 것 같다. 무작정 코드를 짜다보니 중복되는 자료가 많다
