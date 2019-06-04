---
layout: post
title: "[JavaScript][Vanillacoding] 재귀함수 , 클로저 "
date: 2019-06-03
excerpt: "5_week_Mon"
tag:
- JavaScript
- Vanillacoding
category: [Vanillacoding-prep]
feature: https://kyounghwan01.github.io/lala/assets/img/title/bj_title.jpg
comments: false




---


## 5_week_Mon



## Recursion_재귀함수

> 함수는 함수 안에서 자기 자신을 다시 호출하는 것을 재귀함수라고 합니다.
>
> 필요성과 특징에 대해서 알아보겠습니다.

재귀의 필요성은 이해하는 건 쉬운데, 알아보기도 쉽고, 코드의 가독성, 타인이 볼 때 이해도가 높아집니다.
또한 효율적으로 사용의 예로는 **html dom tree 구조 탐색**하는데 쓰입니다.

**factorial 예제**로 살펴보겠습니다
factorial을 알기 쉽게 풀어쓰면

```js
Factorial(5) === 5 * Factorial(4)
Factorial(4) === 4 * Factorial(3)
Factorial(3) === 3 * Factorial(2)
Factorial(2) === 2 * Factorial(1)
Factorial(1) === 1
//위와 같이 풀어 쓸 수 있고
Factorial(n) === n*Factorial(n-1)
// 정리하면 위와 같습니다.
```

위 factorial 예제를 두가지 함수로 작성해보겠습니다.

### iterative vs recursive

먼저 **iterative** 코드를 살펴보면 

```js
function factorial(n){
  let result = 1;
  for(let i = n;i>=1;i--){
    result *=i;
  }
  return result;
}
```

**recursive** 

```js
function factorial(n){
  // Base case, termination case : 결과를 예상할수있는 곳에 끝내는 구간을 설정 
	if( n === 1 ){
    return 1;
  }
  return n * factorial(n-1);
}
```



## recursion 함수 작성법

1. 함수의 순환되는 구조를 파악 
   - factorial의 경우 n을 곱하고 factorial(n-1)이 반복적으로 사용됩니다. 
   - 반복되는 구조를 알기 위해 함수의 진행사항을 코드로 만들어보면 알기 쉽습니다.
2. Base case, termination case : 끝내는 구간을 설정
   - 끝내는 구조를 설정하지 않으면 무한루프에 빠집니다.
   - 위 예제의 경우 `factorial(1)`의 경우 무조건 1이니, 이 조건을 `if`를 통해 걸어주면 끝나는 구간이 설정되어 이후 과정이 시작됩니다.

## recursion 함수 원리

- `Recursion` 함수는 `stack` 원리를 가지고 있습니다.
- `factorial(3)` 이 호출 됬다 가정하면, 

```js
// 먼저 factorial(3)이 실행되고, factorial(3)이 종료되기전 factorial(2)가 실행됩니다. 이때 factorial(3)은 html내 stack에 추가가 됩니다. 
factorial(3) = 3*factorial(2) // 함수 종료 전 factorial(2) 실행
// 동일하게 factorial(2)도 
factorial(2) = 2*factorial(1) // 함수 종료 전 factorial(1) 실행

```

​	위처럼 `factorial(3)` 이끝나기 전에 `factorial(2)` 가 실행되고 끝나지 못한 함수는 `stack` 에 저장됩니다. 
`stack` 의 경우 성질에 따라 먼저 들어간 `stack` 은 후에 들어간 stack이 끝나기 전까지 종료 될수 없습니다.

즉, `factorial(3)` 은 `factorial(2)` 가 종료되기 전까지 종료 되지 않는 다는 의미 입니다.
이에 따라 `factorial` 함수의 끝을 명명하지 않으면 `stack`에 무한정 함수가 추가되어 `error` 를 도출하게 됩니다. 그래서 위에서 쓴 `Base case` 가 꼭 필요한 것입니다.

## recursion 함수 장 단점

장점

- 타 개발자가 알아보기 쉽다. (인간 위주 함수)

단점 

- 브라우저 마다 `stack` 수의 한계가 존재. `stack` 한계 도달시 recursion 사용 못함
- `stack` 은 브라우저의 메모리를 사용한다. 즉, `stack` 을 많이 쓸 수록 웹의 성능 저하 (but 하드웨어의 성능은 좋으니 startup의 경우 해당사항 없음)



아래에서는 재귀 함수가 많이 쓰이는 실제 예제인 **dom 예제**를 보겠습니다.

**DOM traversing 예제**

```html
<body>
	<div>
    <p></p>
  </div>
  	<div>
    <p></p>
  </div>
</body>
<!--재귀 함수에 쓸 예시 DOM 구조 !-->
```

위  작성법과 동일하게 진행

### 1. 함수의 순환되는 구조를 파악 

```js
function logAll(el){
  console.log(el.tagName); // el 태그 이름 콘솔
  if(el.children.length){ // el의 자식태그가 있다면
    for(let i = 0; i < el.children.length; i++){ // 자식태그 수만큼 for문
      const child = el.children[i]; 
      
      console.log(child.tagName); // el의 자식태그 이름 콘솔
      
      if(child.children.length){ // el의 자식의 자식태그가 있다면
        for (let j = 0; j < child.children.length; j++) {
          const grandChild = child.children[j];

          console.log(grandChild.tagName);
          
          //if (){}  ...   
          
          //
      }
    }
  }
}
```

위와 같은 형식으로 console.log , if, for 가 반복적으로 나옵니다. 
다음 console.log 부분에 recursion을 사용하면 될것으로 보입니다.

### 2. Base case, termination case : 끝내는 구간을 설정

중복되는 코드를 기준으로 함수를 다시 실행

```js
function logAll(el){
  console.log(el.tagName);
  // Base case
  if(el.children.length){
    for(var i = 0;i<el.length.length;i++){
      logAll(el.length[i]);
    }
  }
}
logAll(docment.body);
```





## closure

> 클로저(Closure)란, **어떤 함수가 본인이 선언된 주변 환경(변수 etc)을 지속적으로 기억**하는 것을 의미합니다.
>
>  해당 함수가 실행되는 위치가 어디인지에 관계없습니다.

```js
function say(){
  var a = 2;
  function log(){
    console.log(a);
  }
  return log; // 함수 자체를 건내준다
}
var a = say(); // function log(){console.log(a);}
a(); // 2 클로저에 의해 log함수에 접근 할 수  있다. (선언된 함수 기준으로 주변 변수를 가져올 수 있다.)
```

```js
function makeAdder (x) {
  return function add (y) {
    return x + y;
  };
}

var addFive = makeAdder(5);
var addTen = makeAdder(10);

addTen(2); //12 makeAdder안의 add 함수는 클로저에 의해 위치를 파악하고 있고, 바뀌는 x 값도 지속적으로 감시하고 있다. 
addFive(1); // 6 makeAdder 윗 addTen(2)과 별개로 실행됨 
```



js에서 **모든 함수는 본인이 선언된 주변 환경을 기억한다. 함수가 가진 스코프어떻게 변화하는지도 지속적으로 지켜본다**

- 다른 함수 선언에 의해 두번 실행이 되면 우리눈에 함수는 1개지만 코드상 함수는 2개
- 전혀 다른 위치에서 실행해도 원래 함수 본인이 선언된 위치에서 호출이 가능하면 변수 접근 가능
- 더하거나 뺀 것에 대해 변수가 변하는 것도 인지한다.

### 단점 

- closure : 해당 함수의 정보를 계속 관찰 하기에 가능 하다
  -  메모리가 소비된다. 
    - 클로저로인해 성능 이슈가 나올 수 도 있다

- `Garbage collection `
  - 쓸모 없어진 변수를 js엔진이 자동으로 정리해줌
  - 클로저로 변수를 정의하면 garbage collection으로 버려지지 않는다. 
- 즉, 클로저로 어떠한 함수와 스코프에 의해 연관된 변수는 시스템에서 지속적으로 관찰 하고 있다. 



