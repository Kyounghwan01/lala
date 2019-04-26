---
layout: post
title: "[취준] 웹개발 필기테스트 정리"
date: 2018-10-30
excerpt: "제대로 못푼 문제 위주"
tag:
- 취준
category: [ 취준생활 ]
feature: https://png93.github.io/assets/img/title/basic.jpg
comments: true
---

## 목차

* [세션과 쿠키의 차이](#session과-cookie)
* [__encryption과 hashing의 차이__](#encryption과-hashing)
* [__clustered index와 Non clustered index__](#clusteredindex와-nonclusteredindex)
* [스택, 큐, 덱의 차이](#stack)
* outer join
* GROUP BY
* JavaScript
  - [__undefined와 null의 비교__](#undefined와-null)
  - [=== 연산](#일치-연산자)
  - 전위증가, 후위증가 연산
* 정렬 알고리즘

- - -

# session과 cookie
HTTP 연결은 stateless하다는 특징을 갖고 있는데,  
session과 cookie를 사용함으로써 클라이언트와 서버가 연결을 유지하고 있는 효과를 볼 수 있다.  

## 1. session ?
- <hlr>클라이언트와의 연결 상태를 지속적으로 서버측에 저장하는 객체</hlr>
- 웹 브라우저마다 다른 세션을 사용 (session ID로 구분)
- 세션 : 브라우저 = 1 : 1
- 생성 - jsp의 기본객체 중 하나로 별도의 설정을 안했다면 자동 생성됨
~~~
<%@ page session = "true" %>
// 이렇게 페이지 디렉티브에서 설정할 수도 있음, true가 기본값
~~~

- 종료 - 유효시간이 지나면 삭제되고, 다음 요청 때 새로 생성 / 만약 유효시간을 0 또는 음수로 지정했다면 유효시간을 갖지 않게 되므로 반드시 종료를 명시해 주어야 함
~~~
session.invalidate(); // 세션 종료 메서드
~~~

- request 객체를 이용한 session 생성
~~~
<%@ page session = "false" %>
<%
  // session이 존재하면 해당 객체를 리턴, 존재하지 않으면 생성 후 리턴함
  HttpSession httpSession = request.getSession();
%>
~~~

- session을 이용한 로그인
  1. 로그인에 성공하면 session에 특정 속성을 저장한다.
  2. 이후 세션 객체에 특정 속성이 저장되어 있으면 로그인 상태로 간주한다.
  3. 로그아웃시 session.invalidate()를 호출하여 세션 객체를 삭제한다.
~~~
// session에 속성 저장, setAttribute(키, 값);
session.setAttribute("MemberId",id);
~~~


## 2. cookie ?
- <hlr> "웹 브라우저에서 보관하는 데이터"로 웹 서버에 요청을 보낼 때 함께 전송</hlr>
- 이름, 값, 유효시간, 도메인, 경로 로 구성
- __이름, 값__ 이 가장 중요!
- 하나의 브라우저는 여러 개의 쿠키를 저장할 수 있는데 "이름"으로 쿠키를 구분
- "값"은 인코딩 처리 되어 저장
- 유효시간을 별도로 설정하지 않으면 브라우저 종료시 쿠키 삭제
- JSP에서 쿠키 생성 (Cookie 클래스 사용)
~~~
<%
Cookie cookie = new Cookie("Name","value"); //쿠키 객체 생성
response.addCookie(cookie); // 브라우저에 쿠키 정보 전송
%>
~~~

## 3. 차이점 정리
- <hlr>쿠키는 웹 브라우저에 세션은 웹 서버에 저장되는 데이터이다.</hlr>
- 브라우저 : 쿠키 = 1 : 多
- 브라우저 : 세션 = 1 : 1

- - -

# encryption과 hashing

## 1. encryption ?
[암호화]  
- <hlr>'키'를 사용하여 암호화와 복호화를 수행(양방향)</hlr>
- 대칭형 암호화와 비대칭형 암호화가 있음

대칭형 암호화  
- 암호화와 복호화에서 동일한 키(=대칭키)를 공유하는 방법
- 안전하지 않다는 단점이 있음

비대칭형 암호화  
- 공개키와 비밀키 두개를 사용하는 방법
- 대칭형에 비해 안전하지만, 속도가 느림


## 2. hashing ?
- 데이터를 '고정된'길이의 데이터로 매핑하는 방법
- 해시 알고리즘마다 매핑하는 데이터의 길이, 매핑하는 방법이 다양
- <hlr>단방향성 -  암호화만 가능하며 한번 암호화 되면 복호화 불가</hlr>
- 복호화가 필요없는 비밀번호 등에 사용되며, 입력 값에 대해 '해시 값'이 일치하는지에 대한 확인을 수행
- 해싱의 문제점 - 충돌(Collision): 서로 다른 입력 값에 대해 같은 해시 값이 나오는 경우


## 3. 차이점 정리
Encryption은 '키'를 사용하며 '양방향'암호화 방식이고,  
Hashing은 '키'를 사용하지 않으며 '단방향'암호화 방식이다.

- - -

# ClusteredIndex와 NonClusteredIndex
[인덱스]  
- 책의 맨뒤에 '찾아보기'와 같은 역할
- <hly>RDBMS에서 검색 성능을 향상시키기 위해 사용하는 기술</hly>
- Tree 구조로 색인화
- Primary Key 를 생성하면 자동으로 그에 대응하는 인덱스가 생성됨
- SELECT 문의 WHERE절 등에 사용되며, UPDATE, DELETE, INSERT에는 사용되지 않음  
<br/>

[clustered index VS non clustered index]

|                     | Clustered Index | NonClustered Index |
|:--------|:-------:|--------:|
| 테이블 당 최대개수   | 1개   |   249개   |
| 정렬      | 행을 물리적으로 재배열한 결과 저장 |물리적으로 재배열 하지 않음  |
| 인덱스 페이지 용량   |  non clustered 보다 작음   |  clustered 보다 큼   |
{: rules="groups"}

[행을 재배열?]  
clustered index가 생성된 컬럼을 기준으로 정렬된 결과가 DB에 저장된다.  
따라서 데이터를 추가한 순서대로 조회되지 않고 정렬된 결과가 조회된다.

- - -

# Stack
- __LIFO (후입선출) 자료 구조__
- 주요 연산 : 삽입 - push(), 제거 - pop()
- <hlb>콜 스택, 자동 메모리 스택</hlb>

# Queue
- __FIFO (선입선출) 자료 구조__
- 주요 연산 : __Enqueue(Rear에서 수행) , Dequeue(Front에서 수행)__
- 자바에서 제공하는 큐 인터페이스, 주로 링크드리스트 객체로 생성하여 사용
- 메소드: offer(), peek() - 제거X , poll() - 제거O
- <hlb>버퍼</hlb>

# Deque(덱)
- Double-ended Queue
- 양쪽 끝에서 삽입, 삭제 모두 가능한 자료구조
- 스택과 큐를 합친 형태
- <hlb>스케줄링</hlb>

- - -
# undefined와 null
## 1. undefined
자바 스크립트의 자료형 중 하나로 <hly>선언하지 않은 변수</hly> 또는 <hly>선언 했지만 초기화 하지 않은 변수</hly>를 undifined 자료형 이라고 함  
~~~
alert(typeof (variable));
~~~
위와 같은 코드가 실행되면, undefined 라고 출력
* typeof(): 숫자, 문자열, bool 과 같은 자료형을 확인하는 함수  

- 자바스크립트에서 __Boolean(undefined) 는 false__

## 2. undefined와 null의 비교
- 공통점: 둘다 boolean 값이 false이다.
- javascript에서 false 인 자료형에는 __undefined / null / 0 / NaN / ""(빈 문자)__ 가 있다.

~~~
var a;
var b = null;

alert(a); // undefined
alert(b); // null

alert(typeof(a)); // undefined
alert(typeof(b)); // object

alert(Boolean(a));  // false
alert(Boolean(b));  // false

alert(a == b);   // true, "false == false → true"
alert(typeof(a) == typeof(b));  // false, "undefined == object → false"

alert(a === b); // false, a==b → true, typeof(a) == typeof(b) → false 이기 때문에
~~~


- - -
# 일치 연산자
[자바스크립트의 일치 연산자]  
자료형을 확실하게 구분하고자 할 때 사용.  
<hlr>자료형과 값이 모두 일치하는지 확인</hlr>
~~~
=== : 양쪽 자료형과 값이 일치하는지 확인
!== : 양쪽 자료형과 값이 불일치하는지 확인
~~~

~~~
  alert(0 == false);  //true 출력
  alert(0 === false); //false 출력 (좌변은 숫자 자료형, 우변은 bool 자료형)
~~~
