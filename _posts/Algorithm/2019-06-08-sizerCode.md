---
layout: post
title: "[Algorithm] 시저암호"
date: 2019-06-08
excerpt: "시저암호"
tag:
- Algorithm
- for문
category: [Algorithm]
feature: https://kyounghwan01.github.io/lala/assets/img/title/bj_title.jpg
comments: false


---


## 문제 이해

알파벳 대소문자와 공백을 포함한 문자열(s) 1개과 임의의 자연수(n) 1개를  받습니다.

자연수의 숫자만큼 다음 알파벳으로 이동한 문자열을 return 하면 됩니다.
공백은 몇개를 이동해도 공백으로 return 합니다.

Ex) s = "AB d" n = 1 => s = "BC e"

## 문제 해결방법

1. 아스키코드
- for문을 통해 문자열을 검사한다.
- 공백은 공백으로 return 하여 answer에 추가한다.
- 아스키코드를 응용하여 대소문자를 구분하고, n 만큼 코드 수를 더한 후 string으로 되돌린다. 

2. Indexof 함수 응용
- for문을 통해 문자열을 검사한다.
- 공백은 공백으로 return 하여 answer에 추가한다.
- 알파벳 대소문자의 문자열을 나열한다.
- Indexof 함수를 통해 검사한 문자열이 대소문자 문자열에 있는지 스캔한다
- indexof 함수를 통해 문자열이 있다고 판단하면 n을 더한 후 string으로 되돌린다.

## 코드 구현

1. 아스키 코드

```js
function sizer(s,n){
	var s = "ABwefsefgA";
  var n = 25;
  var answer = '';
  for(var i = 0; i<s.length; i++){
    if(s[i] === " "){
      answer += " ";
    }else{
      answer += String.fromCharCode(
        (s.charCodeAt(i)>90)
      ? (s.charCodeAt(i)+n-97)%26+97 : (s.charCodeAt(i)+n-65)%26+65);
    }
  }
  return answer;
}
```

2. Indexof 함수 응용

```js
function sizer(s,n){
	var s = "ABwefsefgA";
  var n = 25;
  var answer = '';
 var alphaCap = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'];
var alphaSmall = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z'];
  
    var input = s.split('');
    var arr = input.map(data => {if(data === " "){
        return " ";
    }
    var Large = alphaCap.indexOf(data);
    var Small = alphaSmall.indexOf(data);

    if(Large > -1){
        Large = (Large + n)%26;
        return alphaCap[Large];
    }
    else{
        Small = (Small + n)%26;
        return alphaSmall[Small]
    }
});
 answer = arr.join('');
}
```



## 결과분석

```
ZAvderdefZ
```

