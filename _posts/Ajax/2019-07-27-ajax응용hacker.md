---
layout: post
title: "[Ajax] Ajax 응용 api로 정보 가져오기"
date: 2019-08-01
excerpt: "Ajax 응용 HeakerNes 카피하기"
tag:
- Ajax
category: [Ajax]
feature: https://kyounghwan01.github.io/lala/assets/img/title/bj_title.jpg
comments: false






---



## Ajax 실행 단계

### 목차

> 1. 해커뉴스 api를 통해 id(key값) 받아오기
> 2. id를 통해 render될 자료를 비동기로 받아와서 dom에 뿌려주기
> 3. 전체 코드
> 4. 완성 예시 : https://kyounghwan01.github.io/Hacker-News/

### 1. 해커뉴스 api를 통해 id(key값) 받아오기

> 해커뉴스 자체적으로 모든 사람들이 사용가능하게 열어 놓은 오픈 api를 활용합니다.
>
> 해커뉴스 홈페이지는 각 페이지당 30개의 리스트를 보여줍니다. 
> 그렇기에 우리도 30개의 리스트를 검색할 30개의 id를 api를 통해 가져옵니다.
>
> 사전에 준비한 카테고리를 배열에 넣고 해당 카테고리별로 30개씩 id 값을 가져옵니다.

- 아래는 id를 가져오는 코드입니다.

```js
let count = 0;

function bringId(num) {
  //해커뉴스 카테고리
  let idArr = [
    "topstories",
    "newstories",
    "askstories",
    "showstories",
    "jobstories"
  ];
  //비동기 작업을 위해 1개의 id당 1개의 XMLHttpRequest객체를 만들어 줍니다.
  let ourRequest = new XMLHttpRequest();
  ourRequest.open(
    "GET",
    `https://hacker-news.firebaseio.com/v0/${idArr[num]}.json?print=pretty`,
    false
  );
  ourRequest.onload = function() {
    newsId = JSON.parse(ourRequest.responseText);
    //newsId에 Id 값이 담깁니다.
  };
  ourRequest.send();
  let last = count + 30;
  if (last > newsId.length) {
    last = newsId.length;
  }
  //count 부터 30개 id를 가져와서 draw 함수에서 실행합니다.
  draw(count, last, num);
}
```



### 2. id를 통해 render될 자료를 비동기로 받아와서 dom에 뿌려주기

```js
function draw(first, last, num) {
  for (let i = first; i < last; i++) {
    // 객체는 클라이언트와 서버 간의 데이터 요청 및 응답 처리를 담당합니다. 
    let ourRequest = new XMLHttpRequest();
    
//open메소드를 사용하여 첫번째 인자로 불러올려면 GET, 내보내려면 POST를 입력, 두번째 인자로 불러올 url 주소를 입력합니다. 요청 매개변수를 초기화하는 메서드로써 URL 에 지정한 서버의 페이지에 어떤 내용을 요청하는데 데이터는 GET/POST 방식으로 보낼 것이고 응답은 동기/비동기로 받을 것이기에 여기에 맞게 XMLHttpRequest 객체를 준비하라는 것과 같습니다.
    
    ourRequest.open(
      "GET",
      `https://hacker-news.firebaseio.com/v0/item/${newsId[i]}.json?print=pretty`
    );
    
    //불러온 데이터를 처리 과정
    ourRequest.onload = function() {
      let Data = JSON.parse(ourRequest.responseText);
      
      // code ...
      
    };

    // HTTP 요청을 실제로 실행하는 메서드입니다. 이 메서드가 실행돼야 비로소 요청이 서버에 전달되기 시작합니다.
    ourRequest.send();
  }
}

```



### 3. 전체 코드

html

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-16" />
    <title>HeakerNews clone Example</title>
    <link rel="icon" href="./img/y.png">
    <link rel="stylesheet" href="./style.css" />
    <div style="margin: auto;">
    </div>
  </head>
  <body>
    <div class="world">
      <div class="header">
          <img class="logo" src="./img/y.png" alt="logo" />
          <ul class="head-title">
            <li><a href="#" class="title">Hacker News</a></li>
            <li class="head-select news"><a href="#">news</a></li>
            <li class="head-select"><a href="#">past</a></li>
            <li class="head-select"><a href="https://news.ycombinator.com/newcomments">comments</a></li>
            <li class="head-select ask"><a href="#">ask</a></li>
            <li class="head-select show"><a href="#">show</a></li>
            <li class="head-select jobs"><a href="#">jobs</a></li>
            <li class="head-select"><a href="https://news.ycombinator.com/submit">submit</a></li>
            <li
              style="float: right;padding-right: 10px;font-size: 20px; line-height: 4.5vh;"
            >
              <a href="#">login</a>
            </li>
          </ul>
      </div>
      <div class="body-container">
        <ol class="ol">
          <div class="blank"></div>
        </ol>
      </div>
      <div class="line">
        <div style="position: relative; top:-30px;left:47px;">
          <span style="font-size:20px;" class="more">More</span>
        </div>
      </div>
      <div class="footer">
        <p class="footer-p"><a href="https://www.startupschool.org/">Registration is open for Startup School 2019. Classes start July 22nd.</a></p>
        <ul>
          <li class="footer-li"><a href="https://news.ycombinator.com/newsguidelines.html">Guideline</a></li>
          <li class="footer-li"><a href="https://news.ycombinator.com/newsfaq.html">FAQ</a></li>
          <li class="footer-li"><a href="#">Support</a></li>
          <li class="footer-li"><a href="https://github.com/HackerNews/API">API</a></li>
          <li class="footer-li"><a href="https://news.ycombinator.com/security.html">Security</a></li>
          <li class="footer-li"><a href="https://news.ycombinator.com/lists">Lists</a></li>
          <li class="footer-li"><a href="https://news.ycombinator.com/bookmarklet.html">Bookmarklet</a></li>
          <li class="footer-li"><a href="https://www.ycombinator.com/legal/">Legal</a></li>
          <li class="footer-li"><a href="https://www.ycombinator.com/apply/">Apply to YC</a></li>
          <li style="font-size: 15px;padding-left: 6px; color: gray;">
            <a href="#">Contact</a>
          </li>
        </ul>
        <div class="footer-search">
          <span class="footer-search-text">Search : </span>
          <input type="text" class="footer-search-input" />
        </div>
      </div>
    </div>
    <script src="./app.js"></script>
  </body>
</html>

```

Css

```css
body {
  margin: 5px 0 10px 0;
}
.header {
  background: rgb(252, 100, 6);
  width: 85vw;
  height: 4vh;
  margin: 0 auto;
}
.logo {
  width: 25px;
  margin: 3px;
  float: left;
}
.title {
  font-weight: bold;
  font-size: 1.2rem;
  padding-left: 5px;
  line-height: 4.5vh;
}
.head-title {
  padding: 0px;
  margin: 0px;
}
.head-title li {
  list-style: none;
  display: inline;
}
.head-select {
  border-right: 1px solid black;
  padding-right: 10px;
  padding-left: 8px;
  font-size: 20px;
  display: inline-block;
}
.head-title li a {
  text-decoration: none;
  color: black;
}
.body-container {
  background: rgb(244, 243, 234);
  width: 85vw;
  height: 1800px;
  margin: 0 auto;
}
.body-container ol {
  margin: 0px;
  padding-left: 0;
  color: gray;
  font-size: 18px;
}
.body-container ol li {
  padding: 0 0 10px 0;
  list-style-type : none 
}
.blank {
  width: inherit;
  height: 20px;
}
.main-title {
  color: black;
  font-size: 20px;
}
.main-sub-title {
  color: gray;
  font-size: 15px;
  text-decoration: none;
}
.main-sub-title a:link {
  color: grey;
  text-decoration: none;
}
.main-sub-title a:hover {
  text-decoration: underline;
}
.main-sub-title a:visited {
  color: gray;
}
.sub-title {
  padding-left: 3.5rem;
  color: grey;
  font-size: 15px;
}
.line {
  width: 85vw;
  height: 2px;
  background: rgb(252, 100, 6);
  margin: auto;
}
.footer {
  background: rgb(244, 243, 234);
  width: 85vw;
  height: 130px;
  margin: 0 auto;
  text-align: center;
}
.footer ul {
  margin: 5px 0 0 0;
  padding: 0;
  height: 10px;
}
.footer ul li {
  display: inline-block;
}
.footer ul li a {
  text-decoration: none;
  color: black;
}
.footer-li {
  border-right: 2px solid gray;
  color: black;
  padding-right: 8px;
  padding-left: 6px;
  font-size: 15px;
}

.footer-search {
  font-size: 20px;
  color: gray;
}
.footer-search-text {
  position: relative;
  bottom: -22px;
}
.footer-search-input {
  width: 180px;
  height: 20px;
  position: relative;
  bottom: -20px;
}
ol li {
  padding: 5px;
}
.footer-p {
  margin: 0 0 0 0;
  padding: 15px 0 12px 0;
  font-size: 1.3rem;
  color: grey;
  text-align: center;
}
.footer-p a:link {
  color: gray;
  text-decoration: none;
}
.footer-p a:visited {
  color: gray;
  text-decoration: none;
}
.link {
  display: inline;
}
.link a:link {
  color: gray;
  text-decoration: none;
}
.link a:hover {
  text-decoration: underline;
}
.link a:visited {
  color: gray;
}
.more{
  cursor: pointer;
}
.list-padding-left{
  padding-left: 1.2rem;
}
.link-title {
  display: inline;
}

.link-title a:link {
  color: black;
  text-decoration: none;
}
.link-title a:hover {
  text-decoration: none;
}
.link-title a:visited {
  color: black;
}
```

JavaScript

```js
const textInput = document.querySelector(".footer-search-input");
const titleBtn = document.querySelector(".title");
const newsBtn = document.querySelector(".news");
const askBtn = document.querySelector(".ask");
const showBtn = document.querySelector(".show");
const jobsBtn = document.querySelector(".jobs");
const ol = document.querySelector(".ol");
let more = document.querySelector(".more");
let newsId;
let count = 0;

textInput.addEventListener("keypress", function(e) {
  if (e.keyCode === 13) {
    location.href = `https://hn.algolia.com/?query=${
      e.target.value
    }&sort=byPopularity&prefix&page=0&dateRange=all&type=story`;
  }
});

function bringId(num) {
  let idArr = [
    "topstories",
    "newstories",
    "askstories",
    "showstories",
    "jobstories"
  ];
  let ourRequest = new XMLHttpRequest();
  ourRequest.open(
    "GET",
    `https://hacker-news.firebaseio.com/v0/${idArr[num]}.json?print=pretty`,
    false
  );
  ourRequest.onload = function() {
    newsId = JSON.parse(ourRequest.responseText);
    console.log(newsId);
  };
  ourRequest.send();
  let last = count + 30;
  if (last > newsId.length) {
    last = newsId.length;
  }
  draw(count, last, num);
}
bringId(0);

function draw(first, last, num) {
  ol.innerHTML = "";
  for (let i = first; i < last; i++) {
    let ourRequest = new XMLHttpRequest();
    let li = document.createElement("li");
    let img = document.createElement("img");
    img.setAttribute("src", "./img/triangle.png");
    img.style = "width: 15px;";
    let listCount = document.createElement("span");
    listCount.classList.add("list-padding-left");
    let mainTitle = document.createElement("span");
    mainTitle.classList.add("main-title");
    let subTitle = document.createElement("span");
    subTitle.classList.add("sub-title");

    ourRequest.onload = function() {
      let Data = JSON.parse(ourRequest.responseText);
      let currentTime = Number(
        new Date()
          .getTime()
          .toString()
          .substr(0, 10)
      );
      let time = Math.floor(currentTime - Data.time);
      let min = 0;
      let hour = 0;
      let DataTime;
      function calTime() {
        if (time > 60) {
          min++;
          time = time - 60;
          calTime();
        } else return;
      }
      calTime();
      if (min > 60) hour = parseInt(min / 60);
      if (hour) {
        if (hour > 1) {
          DataTime = `${hour} hours`;
        } else DataTime = `${hour} hour`;
      } else {
        DataTime = `${min} minutes`;
      }

      let a = document.createElement("a");
      a.href = `${Data.url}`;
      let url;
      if (num === 2) {
        url =
          '<span class="main-sub-title">' +
          "<a href= " +
          `https://news.ycombinator.com/from?site=${a.hostname}` +
          ">" +
          a.hostname +
          "</a></span>";
      } else {
        url =
          '<span class="main-sub-title">( ' +
          "<a href= " +
          `https://news.ycombinator.com/from?site=${a.hostname}` +
          ">" +
          a.hostname +
          "</a>" +
          " )</span>";
      }
      let title = "<a href= " + `${Data.url}` + ">" + Data.title + "</a>";
      mainTitle.innerHTML = ` <span class="link-title">${title}</span> ${url} <br>`;
      listCount.textContent = `${i + 1}. `;
      link = `https://news.ycombinator.com/hide?id=${Data.id}&goto=newest`;
      linkUser = `https://news.ycombinator.com/user?id=${Data.by}`;
      subTitle.innerHTML =
        Data.score +
        " points by " +
        `<p class="link"><a href=${linkUser}>${Data.by}</a></p>` +
        " " +
        `<p class="link"><a href=${link}>${DataTime}</a></p>` +
        " | " +
        `<p class="link"><a href=${link}>hide</a></p>` +
        " | " +
        `<p class="link"><a href=${link}>${Data.descendants} comments</a></p>`;
    };

    li.appendChild(listCount);
    li.appendChild(img);
    li.appendChild(mainTitle);
    li.appendChild(subTitle);
    ol.appendChild(li);
    ourRequest.open(
      "GET",
      `https://hacker-news.firebaseio.com/v0/item/${
        newsId[i]
      }.json?print=pretty`
    );
    ourRequest.send();
  }
}

more.addEventListener("click", function() {
  count = count + 30;
  let last = count + 30;
  if (last > newsId.length) {
    last = newsId.length;
  }
  draw(count, last);
});
titleBtn.addEventListener("click", function() {
  count = 0;
  bringId(0);
});
newsBtn.addEventListener("click", function() {
  count = 0;
  bringId(1);
});
askBtn.addEventListener("click", function() {
  count = 0;
  bringId(2);
});
showBtn.addEventListener("click", function() {
  count = 0;
  bringId(3);
});
jobsBtn.addEventListener("click", function() {
  count = 0;
  bringId(4);
});

```

