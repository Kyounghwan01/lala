---
layout: post
title: "[JavaScript] setInterval / setTimeout / clearInterval"
date: 2019-05-04
excerpt: "setInterval / setTimeout 함수 비교 & 반복 실행 종료 함수 "
tag:
- JavaScript
category: [JavaScript]
feature: https://kyounghwan01.github.io/lala/assets/img/title/bj_title.jpg
comments: false


---

## setInterval

**setInterval()** 함수는 이전 포스팅을 참조 하시기 바랍니다.

[[JavaScript] setInterval 여러 함수 추가하기](https://kyounghwan01.github.io/lala/setInterval/)

- 위처럼 반복해서 사용자가 원하는 바를 실행해주는 메소드가 있다면 그 실행을 중지하는 메소드도 존재합니다.



## clearInterval

**clearInterval()** 함수는 위에 설명한데로 현재 진행되고 있는 함수의 진행을 **멈추는데** 쓰입니다. 

```js
var interval = setInterval(function(){console.log("Interval")},1000);

//인자로 함수 이름 넣어줍니다. 
clearInterval(interval);
```



## setTimeout

**setTimeout()** 함수는 일정시간이 지난 후 인자로 받은 함수를 **한번** 실행해주는 메소드입니다.

```js
//5초 후에 oneTime이라는 string를 콘솔에 1번 찍고 종료합니다. 
setTimeout(function(){
  console.log('oneTime');
},5000);
```
```js
setInterval(function(){
    count++;
    if(count === 10){
        clearInterval(interval);
    }
}, 3000)
```
