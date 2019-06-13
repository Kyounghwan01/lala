---
layout: post
title: "[JavaScript][Vanillacoding] 데이터 가져와서 DOM 그리기"
date: 2019-06-12
excerpt: "6_week_Wen"
tag:
- JavaScript
- Vanillacoding
- DOM
category: [Vanillacoding-prep]
feature: https://kyounghwan01.github.io/lala/assets/img/title/bj_title.jpg
comments: false





---

## 6_week_Wen



## 핵심 원리

> 1. createElements
>    - 새로운 엘리먼트를 만들어서 끼워 넣는다 
>    - `document.createElement('tr') `
>      - `tr` tag를 만든다
>    - appendChild
>      - 만든 태그를 붙인다 `tbody.appendChild(tr)`
> 2. Data attributes (데이터 속성)
>    - `DOM`을 그릴 때, `DOM`에 그릴 자료와 내부에 가지는 데이터를 분리할 필요가 있다. 
>    - ex - 각 엘리먼트가 가지는 `id` 값은 `e.id`로 지정하지 말고 `dataset`을 이용하여 
>      `e.dataset.id` 로 사용하자
>      `id`는 `DOM`을 그릴 때, 사용되는 `id`가 아닌 이상 사용하지 않는 것이 좋다
>
> 3. event 
>    - 이전 포스팅 참조 바람
>
> 4. bug 발생시
>    - 버그가 발생하는 원천지가 어딘지 확인
>    - 버그가 생성되는 과정을 이해하여 `debugger`를 꽂는 것이 중요하다.



## 과정

### HTML & CSS 작업

- 생략

```html
<!doctype html>
<html lang="ko">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width">
    <title>Vanilla Coding | Bootcamp Prep</title>
    <style>
      @import url('https://fonts.googleapis.com/css?family=Lato:300,700&display=swap');

      body {
        margin: 100px 0;
      }

      h1 {
        text-align: center;
        margin-bottom: 100px;
      }

      .main {
        display: flex;
      }

      .main > section, .main > aside {
        width: 50%;
      }

      table {
        border-collapse: collapse;
        font-family: 'Lato', sans-serif;
        font-size: 20px;
        width: 600px;
        text-align: center;
        margin: 0 auto;
      }

      thead {
        background-color: #1E88E5;
        color: #FFFFFF;
        padding: 20px;
      }

      table, th, td {
        border: 1px solid black;
      }

      tbody > tr:hover {
        background-color: #DDDDDD;
        cursor: pointer;
      }

      tbody > tr.highlighted {
        background-color: #DDDDDD;
      }

      th {
        height: 80px;
        font-weight: 700;
      }

      td {
        height: 60px;
        font-weight: 300;
      }

      dl {
        display: flex;
        background-color: white;
        flex-direction: column;
        width: 100%;
        max-width: 700px;
        position: relative;
        padding: 20px;
      }

      dt {
        align-self: flex-start;
        width: 100%;
        font-weight: 700;
        display: block;
        text-align: center;
        font-size: 1.2em;
        font-weight: 700;
        margin-bottom: 20px;
        margin-left: 130px;
      }

      .text {
        font-weight: 600;
        display: flex;
        align-items: center;
        height: 40px;
        width: 200px;
        background-color: white;
        position: absolute;
        left: 0;
        justify-content: flex-end;
      }

      .percentage {
        font-size: 16px;
        line-height: 1;
        width: 100%;
        height: 40px;
        margin-left: 200px;
        background: repeating-linear-gradient(to right, #ddd, #ddd 1px, #fff 1px, #fff 5%);
      }

      .percentage:after {
        content: "";
        display: block;
        background-color: #00BCD4;
        width: 50px;
        margin-bottom: 10px;
        height: 90%;
        position: relative;
        top: 50%;
        -webkit-transform: translateY(-50%);
                transform: translateY(-50%);
        transition: background-color .3s ease;
        cursor: pointer;
      }

      .percentage:hover:after, .percentage:focus:after {
        background-color: #aaa;
      }

      .percentage-5:after {
        width: 5%;
      }

      .percentage-9:after {
        width: 9%;
      }

      .percentage-14:after {
        width: 14%;
      }

      .percentage-17:after {
        width: 17%;
      }

      .percentage-25:after {
        width: 25%;
      }

      .percentage-30:after {
        width: 30%;
      }

      .percentage-51:after {
        width: 51%;
      }

      .percentage-65:after {
        width: 65%;
      }
    </style>
  </head>
  <body>
    <h1>Programming Languages of 2019</h1>
    <section class="main">
      <section>
        <table>
          <thead>
            <tr>
              <th>Languages</th>
              <th>Percentages</th>
            </tr>
          </thead>
          <tbody>
          </tbody>
        </table>
      </section>
      <aside>
        <dl>
          <dt>What <span class="language"></span> Programmers Use</dt>
        </dl>
      </aside>
    </section>
    <script src="./app.js"></script>
  </body>
</html>
```



### JavsScript

1. Data 생성

```js
const DATA = [
  {
    id: "4g2fsfds98dy3hugdi1991h",
    language: "Java",
    percentage: 34,
    editors: [
      {
        name: "IntelliJ",
        percentage: 65
      },
      {
        name: "Eclipse",
        percentage: 17
      },
      {
        name: "Android Studio",
        percentage: 9
      }
    ]
  },
  {
    id: "2y9hfyfyy89hf39ufihfhf",
    language: "JavaScript",
    percentage: 40,
    editors: [
      {
        name: "VS Code",
        percentage: 51
      },
      {
        name: "WebStorm",
        percentage: 30
      },
      {
        name: "Atom",
        percentage: 5
      }
    ]
  },
  {
    id: "349ui0h0239yr9yr0u393298",
    language: "Python",
    percentage: 27,
    editors: [
      {
        name: "PyCharm Prof.",
        percentage: 25
      },
      {
        name: "PyCharm Comm.",
        percentage: 17
      },
      {
        name: "VS Code",
        percentage: 14
      }
    ]
  }
];
```

2. HTML `tag` 및 `class` 가져오기

```js
const $tbody = document.querySelector("tbody");
const $dl = document.querySelector("dl");
const $languageTitle = document.querySelector(".language");
```

3. DATA 활용 `DOM` 만들기

```js
  DATA.forEach(function(data) {
  const $tr = document.createElement("tr");
  const $languageTd = document.createElement("td");
  const $percentageTd = document.createElement("td");

  $languageTd.textContent = data.language;
  $percentageTd.textContent = data.percentage;

  $tr.dataset.id = data.id;
  $tr.appendChild($languageTd);
  $tr.appendChild($percentageTd);
  $tbody.appendChild($tr);
  });
```

4. 클릭 이벤트

```js
  $tr.addEventListener("click", function() {

    const ddAll = document.querySelectorAll("dd");
    if (ddAll) {
      for(let i= 0;i<ddAll.length;i++){
          ddAll[i].remove();
      }
    }

    // 클릭한 데이터 식별
    const languageData = DATA.filter(function(e) {
      return e.id === $tr.dataset.id;
    })[0];

    $languageTitle.textContent = languageData.language;

    //각 언어 에디터를 퍼센트에 맞게 나열하기
    languageData.editors.forEach(function(editor) {
      const $dd = document.createElement("dd");
      $dd.innerHTML = "";
      $dd.classList.add("percentage");
      $dd.classList.add(`percentage-${editor.percentage}`);
      const $span = document.createElement("span");
      $span.classList.add("text");
      $span.textContent = `${editor.name} : ${editor.percentage}`;
      $dd.appendChild($span);
      $dl.appendChild($dd);
    });
  });
```



전체 코드

```js
//그래프에 들어갈 mokdata
const DATA = [
  {
    id: "4g2fsfds98dy3hugdi1991h",
    language: "Java",
    percentage: 34,
    editors: [
      {
        name: "IntelliJ",
        percentage: 65
      },
      {
        name: "Eclipse",
        percentage: 17
      },
      {
        name: "Android Studio",
        percentage: 9
      }
    ]
  },
  {
    id: "2y9hfyfyy89hf39ufihfhf",
    language: "JavaScript",
    percentage: 40,
    editors: [
      {
        name: "VS Code",
        percentage: 51
      },
      {
        name: "WebStorm",
        percentage: 30
      },
      {
        name: "Atom",
        percentage: 5
      }
    ]
  },
  {
    id: "349ui0h0239yr9yr0u393298",
    language: "Python",
    percentage: 27,
    editors: [
      {
        name: "PyCharm Prof.",
        percentage: 25
      },
      {
        name: "PyCharm Comm.",
        percentage: 17
      },
      {
        name: "VS Code",
        percentage: 14
      }
    ]
  }
];

const $tbody = document.querySelector("tbody");
const $dl = document.querySelector("dl");
const $languageTitle = document.querySelector(".language");

DATA.forEach(function(data) {
  const $tr = document.createElement("tr");
  const $languageTd = document.createElement("td");
  const $percentageTd = document.createElement("td");

  $languageTd.textContent = data.language;
  $percentageTd.textContent = data.percentage;

  $tr.dataset.id = data.id;
  $tr.appendChild($languageTd);
  $tr.appendChild($percentageTd);

  $tr.addEventListener("click", function() {

    const ddAll = document.querySelectorAll("dd");
    if (ddAll) {
      for(let i= 0;i<ddAll.length;i++){
          ddAll[i].remove();
      }
    }

    const languageData = DATA.filter(function(e) {
      return e.id === $tr.dataset.id;
    })[0];

    $languageTitle.textContent = languageData.language;

    languageData.editors.forEach(function(editor) {
      const $dd = document.createElement("dd");
      $dd.innerHTML = "";
      $dd.classList.add("percentage");
      $dd.classList.add(`percentage-${editor.percentage}`);
      const $span = document.createElement("span");
      $span.classList.add("text");
      $span.textContent = `${editor.name} : ${editor.percentage}`;
      $dd.appendChild($span);
      $dl.appendChild($dd);
    });
  });

  $tbody.appendChild($tr);
});

```

