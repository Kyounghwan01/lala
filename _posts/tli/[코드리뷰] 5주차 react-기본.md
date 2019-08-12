---
​---
layout: post
title: "[코드리뷰] react 기본"
date: 2019-08-12
excerpt: "5주차 과제 코드리뷰"
tag:
- 코드리뷰
category: [코드리뷰]
feature: https://kyounghwan01.github.io/lala/assets/img/title/bj_title.jpg
comments: false


​---


---



## 1. 인덴팅 , 컨벤션, 주석 (확인 또 확인!)



### 2. Util, Component 분리 

- 각 역할에 따라 디렉토리 분리할 것



### 3. 최대한 함수로 만들어서 이용할 것

- 리터럴한 코딩은 보안에 취약하다 



### 4.  If else 문에서 else 필요 없으면 쓰지 말 것 

```jsx
 if (!page) {
      return;
    } else {
// code ...
    }
```

## 5. 코드 중복 제거 (생각좀하자....)



### 6. [conditional-rendering](https://reactjs.org/docs/conditional-rendering.html)

- 조건부 렌더링

```jsx
const showLoading = this.state.loading ? "display-block" : "display-none";
//이렇게 CSS로 렌더링 조건을 만들지 말고, 조건 자체를 컴포넌트화 시켜서 불필요한 CSS 감소
```

- 보완

```jsx
const showMainPage = this.state.loading ? (
      <div>
        <div className={`App-loading-container`}>
          <img src={logo} alt="" className={`App-loading`} />
        </div>
      </div>
    ) : <Body/>;
```



### 7. 변수의 타입은 최대한 줄이기

```jsx
this.state = {
  page : null,
  //code ...
}
//page는 초기에는 null이었다가 string을 할당 받는다, 그럴바에는 page : ""로 하나의 타입으로 컨트롤 한다.
```



### 8. component 파일 이름은 대문자로



### 9. 함수를 통해 render 할 경우 함수의 이름

```md
bringTopList => renderTopList
bringVideoList => renderVideoList
```



### 10. key값은 id가 들어가는 것이 robust

```jsx
<TopList
	key = {id}
/>
```

