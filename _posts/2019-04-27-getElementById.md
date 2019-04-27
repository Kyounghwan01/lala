---
layout: post
title: "[JavaScript] getElementbyid"
date: 2019-04-27
excerpt: "getElementbyid"
tag:
- JavaScript
category: [JavaScript]
feature: https://kyounghwan01.github.io/lala/assets/img/title/bj_title.jpg
comments: false


---



### 문제 이해

단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다. 마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, **완주하지 못한 선수의 이름**을 return 하도록 solution 함수를 작성해주세요.



### 문제 해결 방법 구상

1. 명단과 완주자의 이름  순서 값이 다르므로 이를 맞추기 위해 오름차순으로 두 배열을 정렬합니다.
2. 명단 배열을 for문 통해 검사하고 for문 안에서는 명단과 완주자의 이름이 같은지 체크하며 다를 시 그 값을 answer로 return 합니다.



### 코드 구현

```javascript
function solution(participant, completion) {
  var participant = ["mislav", "stanko", "mislav", "ana"];
  var completion = ["stanko", "ana", "mislav"];
  var answer = "";

    for(var i=0;i<participant.length;i++){
        if(participant[i]>participant[i+1]){
            var temp =participant[i];
            participant[i]=participant[i+1];
            participant[i+1]=temp;
            i=-1;
        }
    }
    for(var i=0;i<completion.length;i++){
        if(completion[i]>completion[i+1]){
            var temp =completion[i];
            completion[i]=completion[i+1];
            completion[i+1]=temp;
            i=-1;
        }
    }
    //participant.sort(); completion.sort();
    for(var i=0;i<participant.length;i++){
        if(participant[i]!==completion[i]){
            answer = participant[i]      
            break;
        }
    }
    console.log(typeof(answer));
  return answer;
}

solution();
```

### 결과분석

바닐라코드 짜는 것을 우선으로 하기 위해 코드의 효율성 보다는 최대한 원시적인 방법으로 구현하였습니다.

```
"mislav"
```



