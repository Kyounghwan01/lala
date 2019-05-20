---
layout: post
title: "[CSS] transform"
date: 2019-05-19
excerpt: "transform 사용법"
tag:
- CSS
category: [CSS]
feature: https://kyounghwan01.github.io/lala/assets/img/title/bj_title.jpg
comments: false



---

## Interactive_web



## transform

> 기존 position: absolute; 로 인한 배치는 다른 배치된 요소들까지 관여하며, 연산자가 많아 시스템에 부하를 준다. 그에 반해 같은 기능인 transform의 경우 연산자가 적고, 성능이 좋으며 결정적으로 다른 섹터들을 건들이지 않고 css요소를 준 섹터만 영향을 받는다.

### 문법

- 크기

```css
.box : hover{
	transform : scale('배수');
}
```

- 회전

```css
.box : hover{
	transform : rotate("x"deg);
  /*x는 degree, 돌리고자하는 각도를 넣으면 된다.*/
}
```

- 비틀기

```css
/*x 축으로 비틀기*/
.box : hover{
	transform : skew("x"deg);
  /*x는 degree, 돌리고자하는 각도를 넣으면 된다.
  	skew("x"deg, 'y'deg);
  */
}

/*y 축으로 비틀기*/
.box : hover{
	transform : skewY("y"deg);
  /*y는 degree, 돌리고자하는 각도를 넣으면 된다.*/

}
```

- 이동

```css
.box : hover{
	transform : translate(30px, 10px);
  /*x축으로 30px, y축으로 10px 이동*/
}
```

- transform 기준점 변경

```css
.box : hover{
	transform-origin: 0% 100%;
  /*default는 중앙 : 50% 50%*/
}
```

### 종합 예시

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
    <style>
        .box-container{
            display: flex;
        }
        .box{
            width:100px;
            height: 100px;
            background-color: rgba(255,255,0,0.7);
            border: 2px solid black;
            /* 애니매이션 */
            /* 1초동안 호버되는 애니메이션 진행 */
            transition: 2s;
        }
        .box:hover{
            /* 연산자가 적고, 성능이 좋다. 다른 섹터를 건들이지 않음 */
            /* scale() : 크기, rotate("x"deg) : 회전 skew() : x방향 비틀기 skewY() : y방향 비틀기*/
            /* translate(x,y) : x,y방향으로 수치만큼 이동*/
            /* transform: skew(30deg); */
            /* transform: translate(30px, 10px); */
            /* transform의 기준점 변경, default는 중앙*/
            /* transform-origin: 0% 100%; */
            transform: scale(1.5);
            background-color: red;
        }
    </style>
  </head>
  <body>
    <h1>CSS Transform</h1>
    <div class="box-container">
      <div class="box">A</div>
      <div class="box">B</div>
      <div class="box">C</div>
      <div class="box">D</div>
      <div class="box">E</div>
    </div>
  </body>
</html>

```

##  
