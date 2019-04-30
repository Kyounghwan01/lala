---
layout: post
title: "[Algorithm] 직사각형 별찍기"
date: 2019-04-29
excerpt: "가로,세로 길이 주어질 때 직사각형 형태로 * 출력"
tag:
- Algorithm
- for문
category: [Algorithm]
feature: https://kyounghwan01.github.io/lala/assets/img/title/bj_title.jpg
comments: false


---

## 문제 이해

이 문제에는 표준 입력으로 두 개의 정수 n과 m이 주어집니다.
별(*) 문자를 이용해 가로의 길이가 n, 세로의 길이가 m인 직사각형 형태를 출력해보세요.



## 문제 해결 방법 구상

1. n값이 주어지면 n의 수만큼 "*"을 출력하고 m의 수만큼 띄어쓰기를 한다.



## 코드 구현

```javascript
function solution(n,m) {
  var n=5;
  var m=3;
  var result="";
  for(var i=0;i<m;i++){
    for(var j=0;j<n;j++){
      result+="*";
    }
    result+="\n";
  }
}
solution();
```

## 결과분석

2중 for문으로 m=0일때, n값 만큼 *를 더하고 for문을 탈출하여 띄어쓰기를 하고 다음 m=1,2,3,4,5~ 일때 반복하여 실행한다.

```
"
*****
*****
*****
"
```



