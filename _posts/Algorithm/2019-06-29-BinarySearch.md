---
layout: post
title: "[Algorithm] BinarySearch"
date: 2019-06-29
excerpt: "programmers BinarySearch"
tag:
- Algorithm
category: [Algorithm]
feature: https://kyounghwan01.github.io/lala/assets/img/title/bj_title.jpg
comments: false



---

##  

## 문제 이해

> arr이 주어질때, value의 arr 없다면 -1을 return 하고 <br>
> value의 값이 arr에 있다면 이진탐색으로 value를 찾고, value를 찾는 경우의 수를 return 하시오 <br>
> Ex) arr = [0,1,2,3,4,5,6,7,8,9,10 … ,100], value = 3; answer = 6 (6번만에 3를 찾는다)

## 문제 해결방법

1. 100중의 3의 위치를 50을 기준으로 위아래를 찾는다. 
2. 3은 50보다 작으므로 다시 25를 기준으로 위아래로 3의 위치를 찾는다
3. 3은 25보다 작으므로 12를 기준으로 위아래로 3의 위치를 찾는다.
4. 계속 반복하여 3의 위치를 찾는다.
5. 상,중,하를 변수로 두고 값이 반보다 클경우 값보다 작은 배열을 자른다.
6. 값이 없을 경우 -1 리턴 

## 코드 구현

```js
var arr = [];
for(let i = 0; i<100;i++){arr.push(i);}

function binarySearch(arr,value){
  let low = 0;
  let mid = 0;
  let high = arr.length-1;
  let count = 0;

  while(low <= high){
    mid = Math.floor((low + high)/2);
    if(arr[mid] === value){
      count++;
      return console.log(count);
    } else if(value > arr[mid]){
      low = mid +1;
      count++;
    }else{
      high = mid -1;
      count++;
    }
  }
  return console.log(-1);
}

binarySearch(arr,3);

```

## 결과

```js
6
```

