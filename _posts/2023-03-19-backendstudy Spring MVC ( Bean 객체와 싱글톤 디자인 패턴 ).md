---
layout: single
title: "Spring MVC"
toc: true
toc_sticky: true
toc_label: "목차"
categories: backendstudy
toc_icon: "bars"
tags: [backendstudy]
---

📘Spring MVC ( Bean 객체와 싱글톤 디자인 패턴 )

# 스프링 컨테이너란?
- 자바 객체의 생명 주기를 관리하며, 생성된 자바 객체들에게 추가적인 기능을 제공하는 역할을 한다
- Ioc,DI의 원리가 스프링 컨테이너에 적용된다
- 개발자는 new 연산자, 인터페이스 호출, 팩토리 호출 방식으로 객체를 생성하고 소멸 시킬수 있는데, 스프링 컨테이너가 이 역할을 대신해 줍니다. 
- 제어 흐름을 외부에서 관리하는 것
- 객체들 간의 의존 관계를 스프링 컨테이너가 런타임 과정에서 알아서 만들어 준다
- 여기서 말하는 자바 객체를 스프링에서는 Bean이라고 부른다

# Bean 객체
- Spring IoC컨테이너가 관리하는 자바 객체를 빈(Bean)이라고 부른다

> 제어의 역전 IOC의 
> 객체의 생성을 특별한 관리 위임 주체에게 맡긴다. 이 경우 사용자는 객체를 직접 생성하지 않고 , 객체의 생명주기를 컨트롤하는 주체는 다른주체가 된다.

- Spring에서는 직접 new를 이용하여 생성한 객체가 아니라, Spring에 의하여 관리당하는 자바 객체를 사용합니다.
- 이렇게 Spring에 의하여 생성되고 관리되는 자바 객체를 Bean이라고 한다.
- Spring Bean 을 얻기 위하여 ApplicationContext.getBean()와 같은 메소드를 이용한다