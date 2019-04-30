---
layout: post
title: "[Algorithm] 피보나치 수"
date: 2019-04-26
excerpt: "피보나치 수 구하기"
tag:
- Algorithm
- for문
category: [Algorithm]
feature: https://png93.github.io/assets/img/title/bj_title.jpg
comments: false
---



### 문제 이해

피보나치 수는 앞에 있는 두 수의 합이 현재의 수가 되는 규칙을 가지는 수 입니다.

| 0    |  1   |  2   |  3   |  4   |  5   |  6   |  7   |  8   |  9   |  10  |  ... |
| :--- | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | ---: |
| 0    |  1   |  1   |  2   |  3   |  5   |  8   |  13  |  21  |  34  |  55  |  ... |



<br/>

### 문제 해결 방법 구상

1. 조건에 n이 2이상이라 주어졌기 때문에, f배열에 0,1,2번째는 임의로 삽입합니다.
2. n번째까지의 피보나치 수를 구하기위해 i는 3부터 n번까지 for문으로 처리합니다.
3. for문 내부 함수는 i번째는 i-1번째와 i-2번째를 더한 값에 그 값을 1234567로 나눈 값을 부여합니다.



### 코드 구현

```javascript
function sol(n){
    var n =1234568;
    var answer=0;
    f=[0,1,1];
    for(var i=3;i<=n;i++){
        // 0,1,1,2,3,5,8,13
     f[i]=(f[i-1]+f[i-2])%1234567
    }
    console.log(f[n])
    
    answer=f[n]
    console.log(answer); 
}
sol();
```

### 결과분석

오류 없습니다.
