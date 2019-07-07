---
layout: post
title: "[JavaScript] var/let/const 차이"
date: 2019-07-07
excerpt: "var/let/const 차이"
tag:
- JavaScript
category: [JavaScript]
feature: https://kyounghwan01.github.io/lala/assets/img/title/bj_title.jpg
comments: false









---



## var/let/const 차이

var let const를 비교할 때 몇가지 키워드로 정리해서 알아보자

1. 변수 값의 변환
2. 변수의 유효범위
3. 호이스팅



### 1. 변수 값의 변환

기존의 js를 사용하면서 가장 문제가 있다고 느낀점은 변수 선언의 방식이였다.
var를 사용하면 변수 선언의 경우 할당되는 값이 유동적으로 변경될 수 있다는 단점이 있다.

```js
var name = "noh";
console.log(name); //noh
var name = "ki";
console.log(name); //ki
```

이와 같이 name이라는 변수를 2번 선언했는데도 에러가 나오지 않고 각기 다른 값이 출력되는 것이 보인다. 

하지만 let,const는 var와 같은 선언 방식을 막고 있다.

```js
let name = "noh";
console.log(name);  //noh

let name = "ki";
console.log(name);
//Uncaught SyntaxError: Identifier 'name' has already been declared at <anonymous>:1:1
```

위와 같이 let을 사용했을 경우 name이 이미 선언되었다는 에러가 나오는 것을 볼 수 있다.

let과 const의 경우로는 둘다 위와 같이 **변수 재선언**은 둘다 불가하지만
let의 경우 **재할당**이 가능하고, const는 **재할당이 불가**하다.

```js
let name = "noh";
console.log(name);  //noh
name = "ki";
console.log(name); //ki

const name ="noh";
console.log(name); //noh
name = "noh" // Uncaught TypeError:Assignment to constant variable.
```



### 2. 변수의 유효범위

var는 기본적으로 function scope를 가지게 되고,
let,const는 block scope를 가진다.

```js
var foo = "string";
if(typeof foo === 'string'){
	var result = true;
}else{
  var result = false;
}
console.log(result)  // true
```

```js
var foo = "string.";
if(typeof foo === 'string'){
    const result = true;
} else {
  const result = false;
}

console.log(result);    // result is not defined
```



### 3. 호이스팅

var

```js
const hoisting = () => {
     var name; // name 변수는 호이스트 되었습니다. 할당은 이후에 발생하기 때문에, 이 시점에 name의 값은 undefined 입니다.
     console.log("First name : " + name); // First Name : undefined
     name = "Marcus"; // name에 값이 할당 되었습니다.
     console.log("Last Name : " + name); // Last Name : Ford
}
```

 var는  **변수가 함수내에 정의 되었을 경우 선언이 함수의 최상위로, 함수 바깥에서 정의될 경우 전역 변수로 정의됩니다**

let 

```js
const hoisting = () => {
  console.log("Name:", name);
  let name = "Marcus";
}

hoisting();
// ReferenceError: name is not defined
```

let, const의 경우 같은 예시에서 not defined 에러가 도출되는데 이 이유를 알려면
Temporal Dead Zone(TDZ)의 개념을 알아야 합니다.

let/const 선언은 기본적으로 실행중인 실행 컨텍스트의 어휘적 환경(Lexical Environment)으로 범위가 지정된 변수를 정의합니다.

새로운 범위에 진입할 때마다 지정된 범위에 속한 모든 let/const바인딩이 지정된 범위 내부의 코드가 실행되기 전에 실행됩니다.. (즉, let/const선언이 호이스팅된다.)
어휘적 바인딩(변수선언)이 실행되기 전까지 액세스할 수 없는 현상을 TDZ라고 합니다.

쉽게 말해 스코프에 진입할 때 변수가 만들어지고 TDZ가 생성되지만, 코드 실행이 변수가 실제 있는 위치에 도달할 때 까지 액세스 할 수 없는 것입니다.

TDZ를 이해한바를 코드로 작성하면

```js
function tdz(){
  console.log(TDZ); //Cannot access 'TDZ' before initialization
  let TDZ = "tdz"; //이 코드 실행 후
  console.log(TDZ); //TDZ에 접근 가능하다.
}
```



그래서 결론은!

let/const으로 선언한 변수가 호이스팅 안되는 것은 아니다. 스코프에 진입할 때 변수가 만들어지고 TDZ가 생성되지만, 코드 실행이 변수가 실제 정의된 위치에 도달할 때까지 액세스 할 수 없기에 호이스팅이 안되는 것 처럼 보일 뿐이다. let/const 변수가 선언된 시점에서 제어 흐름은 TDZ를 떠난 상태가 되며, 변수를 사용할 수 있게 됩니다.
