---
layout: single
title: "리스너와 필터,RESTAPI"
toc: true
toc_sticky: true
toc_label: "목차"
categories: web
toc_icon: "bars"
tag: [web]
---

📘웹서비스프로그래밍

# Listener
- 컨테이너에서 발생하는 이벤트를 모니터링하다가 특정 이벤트가 발생하면 실행되는 특수한 서블릿. 이벤트 리스너라고도 함
- 웹 애플리케이션 실행에 필요한 정보를 제공하거나 톰캣 시작/종료와 같은 특정 상황에 자동으로 동작하는 프로그램을 구현할 때 사용
- 리스너는 일반적인 형태의 서블릿이 아니라 특정 이벤트에 따라 동작하는 인터페이스를 구현한 클래스
- 리스너가 동작하기 위한 이벤트의 종류와 그에 따른 프로그램 API를 알아야함

## 리스너의 유형
1. 초기화 매개변수와의 연동
2. 예제 프로그램 등을 배포할 때 샘플 데이터 제공
3. 복잡한 환경 설정 제공
4. 특정 이벤트에 동작하는 기능 구현

# 필터
- 서블릿 필터라고도 하며 리스너와 마찬가지로 웹 애플리케이션을 지원하기 위한 특수한 형태의 서블릿
- 클라이언트 요청에 따라 서블릿이나 jsp가 실행되기 전에 response 혹은 request 객체의 조작이나 추가적인 처리
- 필터는 기본적으로 특정 요청에만 동작하며, 여러 개의 필터가 정해진 순서에 다라 배치될 수 있는데 클라이언트 요청 처리 이전에 먼저 실행됨
- 필터는 톰캣 서버를 시작할 때 필터 구현 클래스의 애너테이션을참조하여 클래스 초기화
- 여러개 존재 가능 

## 필터 활용 분야
1. 인증 : 기존 소스를 최대한 수정하지 않고 인증 기능 수행
2. 로킹/감사 : 해당 요청을 수행하기 전 로깅 처리
3. 국제화 : 특정 페이지에 들어갈 메시지 등을 해당 언어로 변환하여 전달
4. 한글 인코딩 처리 : 한번에 한글 인코딩 처리

# RESTAPI
- REST : 하나의 Resource는 여러 형태의 Representation(json,xml,test,rss)으로 전달할 수 있다는 개념

- 등장 배경
1. 클라이언트-서버 프로그램 구조의 문제점 등장
    - 동시 다중 접속에 대한 안정성, 보안, 백업, 장애 대응 , 이중화 등 여러 기술적 문제를 자체적으로 해결할 수 있는 역량과 고수준의 개발자와 서버 엔지니어 필요
    - 클라이언트와 통신을 위해 요청,응답,메시지 규격 등 프로토콜을 자체적으로 정의해야 함
    - 전용 프로토콜 사용으로 서비스 간 호환 어려움
2. 웹을 사용하는 것으로 상당 부분 해결 가능
3. 웹은 기본적으로 클라이언트 요청에 대한 응답으로 화면 중심의 html을 제공하는 시스템이기 때문에 단순히 데이터를 주고받고자 하는 서비스에는 적합하지 않음
4. 확정성이 뛰어나고 경량의 데이터 구조라고 할 수 있는 json이 주목을 받기 시작함 
5. RESTfull개념이 재조명되어 본격적으로 적용되기 시작해 지금의 프런트엔드 중심 개발을 이끌게 됨

## JAX-RS
- Java Api for RESTful Web Services
- REST서비스를 제공하기 위해서 여러 HTTP Method를 지원하면서 다양한 URI 요청을 처리할 수 있는 서버 프로그램 구조 필요
- 서블릿만 이용해도 어느정도 REST형태의 서비스를 개발할 수 있지만 여러 URI요청을 구조적으로 손쉽게 처리하려면 규격이필요함
- REST 원칙을 사용하는 개발 메커니즘을 제공하는 자바 표준 api
