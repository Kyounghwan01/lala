---
layout: post
title: "[JavaScript][Vanillacoding] Primitive / Reference"
date: 2019-04-30
excerpt: "2_week_Mon"
tag:
- JavaScript
- Vanillacoding
category: [Vanillacoding-prep][JavaScript]
feature: https://kyounghwan01.github.io/lala/assets/img/title/bj_title.jpg
comments: false



---

## 2_week_Mon

## contents

1. [Primitive](#Primitive)
2. [Reference](#Reference)

## Primitive

#### 의미 

- 원시적인

#### 종류

1. number 

   1. ```js
      var num = 7; var num1 = 7;
      if(num===num1) //true => 원시적이다.
       //var num이 6으로 바뀌면 7로 쓰였던 문자열 데이터는 버려지고 6으로 새로운 데이터가 만들어 진다.
      ```

2. boolean

3. string

4. null

5. undefined

## Reference

#### 의미 

- 어떠한 변수에 할당하면 컴퓨터의 메모리에 저장이 되는데 reference에 해당하는 값들은 데이터의 값을 담는게 아니라 데이터가 담긴 위치 값을 할당 받는다. => **참조값** 

#### 이해 

-  이메일 주소를 적으려한다. 포스트잇은 너무 작아 다 못적으니 책상 두번째 서랍 a4종이에 적고 포스트잇에는 책상 두번째 서랍이라는 위치를 적는다. 복사를 띄고 책상 세번째 서랍에 보관한다.
  - 복사본과 원본의 값은 같으나 포스트잇의 **주소 값은 다르기**에 두 값을 비교하면 false 출력

#### 종류

1. object

   1. ```javascript
      var a-{age:3};
      var b={age:5};
      var mother={
      	age:55,
      	children:[a,b]
      };
      a.age++;
      b.age++;
      console.log(mother.children); //[{age:4},{age:6}]
      ```

2. function

3. array

   1. ```js
      var list=[1,2,3]; 
      var list2=[1,2,3];
      
      list1===list2; //false
      
      var list3=[1,2,3]; //list3 에 담긴 값은 배열의 위치다
      var list4=list3; //list3의 주소를 복사한다.
      list3===list4; //true 
      
      var obj1={num:1};
      var obj2=obj1;
      obj1.num++;
      console.log(obj2); //2 (위치 공유되기때문에 obj1,2는 같이 변한다.)
      ```

#### 활용

```js
/*활용
과거 데이터의 위치를 저장하고 그 데이터를 다른 값으로 바꾼 후 이전 데이터와 비교할 때 사용한다.
*/

var childern = mother.children; // var 에 임시적으로 위치를 저장한다.
mother.children = father.childern // 새로운 위치 저장, 위와 아래 비교
```
