---
layout: post
title: "[CSS] transform keyframes"
date: 2019-05-20
excerpt: "keyframes 사용법"
tag:
- CSS
category: [CSS]
feature: https://kyounghwan01.github.io/lala/assets/img/title/bj_title.jpg
comments: false



---

## Interactive_web



## transform keyframes

> 애니메이션을 위한 timeline을 지정함
>
> 시작점 : 0%
>
> 끝점 100%

### 문법

- 움직일 box모형을 먼저 정의 함 

```css
.box{
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100px;
    height: 100px;
    border: 2px solid #000;
    background-color: #fff000;
 }
```

- Keyframes 정의

```css
@keyframes sample-ani{
        /* timeline : 시작점 : 0%, 끝점 : 100% %로 키프레임 지정 */
        0% {
          /* 이동을 안함 */
          transform: translate(0,0); 
        }
        50%{
          background-color: blue;
          transform: translate(300px,0);
        }
        100%{
          transform: translate(400px,500px);
        }
      }
```

- 정의한 박스 css에 keyframes 추가

```css
.box{
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100px;
    height: 100px;
    border: 2px solid #000;
    background-color: #fff000;
    animation: sample-ani 3s linear forwards;
 }
```

- 이동에 대한 속성은 개발자 모드에서 콘솔창으로 확인 가능

```css
animation: sample-ani 3s linear;
	  /*애니메이션 작동 시간*/
    animation-duration: 3s;
	  /*애니메이션 이동 패턴 : linear : 등운동, default : 자연스러움*/
    animation-timing-function: linear;
		/*value 초 후 애니메이션 작동*/
    animation-delay: 0s;
		/*몇번 실행하는지, infinity, 3 ...*/
    animation-iteration-count: 1;
		/* alternate : 0%~100%갔다가 100%~0%로 이동 ,reverse도 가능 */
    animation-direction: normal;
		/* animation-fill-mode : 애니 종료시 box어디에 둘것인지 forwards : ani 종료시 100%에 고정됨 */
    animation-fill-mode: none;
		/*조건을 지정한 후 해당 css에 animation-play-state: paused 로 일시정지*/
    animation-play-state: running;
    animation-name: sample-ani;
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
    <title>Interactive Web</title>
    <style>
      @keyframes sample-ani{
        /* timeline : 시작점 : 0%, 끝점 : 100% %로 키프레임 지정 */
        0% {
          /* 이동을 안함 */
          transform: translate(0,0); 
        }
        50%{
          background-color: blue;
          transform: translate(300px,0);
        }
        100%{
          transform: translate(400px,500px);
        }
      }
       .box{
         display: flex;
         align-items: center;
         justify-content: center;
         width: 100px;
         height: 100px;
         border: 2px solid #000;
         background-color: #fff000;
         /* 만든 키프레임 적용 */
         /* infinite : 횟수무한 반복, 숫자로 변경 가능 */
         /* alternate : 0%~100%갔다가 100%~0%로 이동 ,reverse도 가능 */
         /* animation-fill-mode : 애니 종료시 box어디에 둘것인지 forwards : ani 종료시 100%에 고정됨 */
         animation: sample-ani 3s linear forwards;
       }
       .box:hover{
         /* animation-play-state : 애니 이동시 어떻게 제어할 것인지*/
         animation-play-state: paused;
       }
        /* 애니메이션은 keyflame지정 가능 : 방향의 변화를 주는 지점 */
    </style>
  </head>
  <body>
    <h1>Animation</h1>
    <div class="box">Box</div>
  </body>
</html>
```

