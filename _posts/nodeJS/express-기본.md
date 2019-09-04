---
layout: post
title: "express 기본"
date: 2019-09-02
excerpt: "express 기본"
tag:
- JavaScript
- Vanillacoding
- nodeJS
category: [nodeJS] 
feature: https://kyounghwan01.github.io/lala/assets/img/title/bj_title.jpg
comments: false





---

## express

> node.js와 같이 가장 많이 사용되는 express에 대해 살펴보도록 하자	<br>
>
> 일단 express를 사용하는 가장 큰 이유는 **에러 핸들러**를 가장 잘 지원을 하기 때문이다 <br>
>
> 서버에서는 에러핸들러가 가장 중요하다. 서버는 DB와 연관이 있고 그것은 곳 보안이기 때문이다. 그렇기 때문에 에러 핸들러를 어떻게 하냐에 따라 앱의 성능이 달라지게 된다.<br>
>
> 서버 구축의 가장 기본적인 부분을 살펴본다. <br>이외 궁금한 사항은 expressjs 홈페이지에서 참조하면된다,

### express-generator

> 스스로 서버를 구축해야할 때, `express-generator`를 사용한다. <br>express에서 html 템플릿엔진은 ejs, pug, handlebar 3중 1개를 골라 쓴다.<br>css 전처리 과정 가능 하다 (less, sass 등등..)<br>`--git`커멘드를 통해 모듈파일이 git에 올라가지 않게 막을 수 있다. 

### 서버 구축 과정

1. `express --view=ejs --css=less --git sample `
2. 만든 dir 가서 `npm install`
3. `package.json`관찰
   1. dependencies : 실제 어플이 구동될때 진짜 필요한 모듈
   2. Dev-dependencies : 개발 환경에 필요한 모듈 : test모듈
   3. Scripts : key를 커멘드로 치면, value 커멘드가 실행됨
4. `bin/www` 가 서버 구동 파일 (`www`가 서버 컨벤션) (왠만하면 서버 파일은 조작하지 않도록 하자) 
5. 작업은 `app.js`에서 한다
   1. middleWare
   2. error-handling



### middleWare

> express는 라우팅 및 미들웨어 웹 프레임워크이며, express app은 기본적으로 일련의 미들웨어 함수 호출로 data의 이동이 이루어진다. <br>그러므로 미들웨어에 대한 개념을 숙지하는 것은 매우매우매우매우 중요하다. 
>
> 미들웨어 함수는 `req, res, next`3가지 prarms를 기본으로 갖추게 된다. 

애플리케이션 레벨 미들웨어

`app.use()`, `app.method()`함수를 이용해 미들웨어를 사용한다. <br>이때 `method`함수는 `GET`,`PUT`,`POST`등등 소문자로 된 `HTTP` 메소드이다.

1. `use`

라우트의 path를 주고 함수를 넣거나, 바로 함수를 넣는다.

```js
//함수를 넣는 것이 keypoint!
app.use('/',index);
app.use(function(req){
  //code...
})
```

2. `method`

```js
app.get('/user/:id', function (req, res, next) {
  res.send('USER');
});
```



3. 미들웨어는 꽃는 순서가 중요하다

미들웨어는 stack 구조로 `app.js` 내에서 줄을 서는데

`logger -> bodyparser -> cookie parser -> less -> static -> './' -> /users -> 404`로 코드를 작성했다 가정했을 때, 만약 어떤 요청이 들어오면 (`GET '/'`)

요청은 위의 **순서대로** 거쳐 지나다가 res를 진행하는 곳(`'/'`)'에서 처리가 끝난다.



4. `bodyParser.json()`

`req.body`를 개발자가 보기 좋게 요청을 받아주는 모듈, 보통 doc에 어디보다 선행하라고 기술함



5. `next()`

다음 미들웨어를 실행하도록 trigger하는 함수 

```js
app.use(function(req,res,next){
  if(req.params.use_id){
    //1. 여기가 호출되면
    next();
  } else {
    //3. next함수에 인자를 넣어주면 에러로 취급하고 다음 줄 선 함수 모두 무시하고 맨 마지막의 에러 미들웨어를 호출한다.
    //next(new Error());
    next(123);
  }
});

//2. 여기가 호출됨
app.use(function(req,res,next){
  next();
})

//4. 맨 마지막 미들웨어는 무조건 에러 핸들링 미들웨어 (custom error handler)
// 여러개의 에러 핸들러 가능하다
app.use(function logging(err, req, res, next){
  console.log(err) //123
  next(err);
})
app.use(function (err, req, res, next) {
  console.error(err.stack)
  res.status(500).send('Something broke!')
  //여기가 최종 핸들러인데 next가 의미하는 바는? default error handler를 부른다.
})
```



서버는 에러가 나면 프론트엔드 코드등 클라이언트에 에러가 났다 왜 났다 라는 응답을 줘야한다. 

클라이언트에 대략적인 에러의 원인을 알려야 한다 (http 에러 코드 정도(400, 500))



### logging 

로그를 남긴다. 서버 사용한 서버 로그 기록을 남긴다.

에러 추적하기 위함



### 환경변수

#### 왜 필요한가? 

- 코드와는 별개로 보안에 관련된 정보를 외부의 변수값을 설정하여 쓸 때

#### 어떻게 쓰는가?

`process.env` 객체에는 환경변수가 key, value로 들어가 있다.

1. node 명령어 앞에 환경변수 key, value를 정의한다.

```js
scirpt : {
  start : SC = 123, nodemon ...
}
```

2. dotenv 사용

