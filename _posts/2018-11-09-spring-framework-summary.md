---
layout: post
title: "[취준] 기술 면접 대비 Spring 정리"
date: 2018-11-09
excerpt: "Spring Framework 요약 정리"
tag:
- 취준
category: [ 취준생활 ]
feature: https://png93.github.io/assets/img/title/basic.jpg
comments: true
---

## Spring의 주요 기능 / 특징
1. [MVC](#spring-mvc)  
2. [DI](#di)  
3. [AOP](#aop)  
4. [POJO](#pojo)
- - -

# Spring MVC  

* MVC: 웹 어플리케이션 개발 디자인 패턴

- MVC는 __Model / View / Controller__ 의 약자
- model, view, controller 들이 유기적으로 동작
- <hlr>개발자가 직접 컴포넌트를 호출하지 않아도 자동으로 불러주며, 반복적인 작업을 줄여줌</hlr>
- 따라서 개발자는 핵심 로직에 집중할 수 있음

__[Spring MVC의 처리 과정]__  

![](https://png93.github.io/assets/img/post/spring_mvc_flow.PNG)  

1. DispatcherServlet이 클라이언트로 부터 요청을 받음
2. HandlerMapping을 통해 요청에 해당하는 Controller를 찾고
3. 해당 Controller로 요청을 보냄
4. Contoller에서 작업을 수행한 후 ModelAndView를 반환
5. ViewResolver에서 사용자에게 보여줄 View를 결정
6. DispatcherServlet이 View를 호출
7. 클라이언트에 해당 View가 보여짐

- - -

# DI
[Dependency Injection, 의존성 주입]  
<hlr>객체간의 의존 관계를 객체 자신이 아닌 외부 조립기가 수행해 주는 개념</hlr>

1. Setter Injection
  - xml 설정파일에 \<property\> 이용하여 설정
2. Construction Injection
  - xml 설정파일에서 \<constructor-arg\> 에 설정
  - 또는 \@Autowired 어노테이션 이용해서 수행 할 수 있음

- - -

# AOP

[Aspect Oriented Programmin, 관점 지향 프로그래밍]  
- JAVA의 경우 다중 상속이 불가능 하기 때문에 공통 기능을 상속 받는 것에 한계가 있는 경우가 생김
- __OOP 만으로 해결할 수 없는 의존관계의 복잡성과 코드 중복을 해결하기 위한 방법__
- 핵심 기능과 공통기능을 분리하여,  
공통 기능을 필요로 하는 핵심 기능들에서 사용하는 방식
- __공통 모듈을 여러 코드에 적용하는 기법__

- - -

# POJO

[Plain Old Java Object]  
스프링 컨테이너에 저장되는 자바 객체는 특정한 인터페이스를 구현하거나 클래스를 상속받지 않아도 된다.  
따라서 기존에 작성한 클래스를 수정할 필요 없이 스프링에서 사용할 수 있다.
