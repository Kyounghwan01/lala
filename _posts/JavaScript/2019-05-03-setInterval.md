---
layout: post
title: "[JavaScript] setInterval 여러 함수 추가하기"
date: 2019-05-03
excerpt: "setInterval 함수에 여러 함수를 인자로 넣어서 실행"
tag:
- JavaScript
category: [JavaScript]
feature: https://kyounghwan01.github.io/lala/assets/img/title/bj_title.jpg
comments: false


---

## setInterval

**setInterval()** 함수는 주기적으로 인자를 실행하는 함수입니다.

- 보통 아래와 같이 사용합니다.

```js
//Hello!라는 문자열을 콘솔에 3초에 1번씩 실행합니다.
function test(){
  console.log("Hello!");
}
setInterval(test, 3000);
```

- 위 test 함수에 인자가 있다면?

```js
function test(string){
  console.log(string);
}
setInterval(function(){test("Hello!")}, 3000);
```

- 위 방법을 응용하여 여러 함수를 인자로 넣어서 실행해 봅시다!

```js
function test1(string){
  console.log("test1 : " + string);
}

function test2(string){
  console.log("test2 : " + string);
}

setInterval(function(){
  test1("Hello!"); 
  test2("World!")
}, 3000);
//위와 같이 setInterval 함수 안에 함수를 인자로 넣고 실행하면 두개의 함수가 3초에 한번씩 실행됩니다. 
```

```html
test1 : Hello!
test2 : World!
test1 : Hello!
test2 : World!
```

