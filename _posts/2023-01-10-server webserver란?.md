---
layout: single
title: "web server란?"
toc: true
toc_sticky: true
toc_label: "목차"
categories: server
toc_icon: "bars"
tags: [server]
---

📘웹서버 

# web server
웹서버(web server) : 주로 정적 콘텐츠(이미지나 정적 HTML 등)를 제공하기 위해 설계되었으며 
동적 콘텐츠 요청을 식별하여 was(Web Application Server)로 요청을 전달하는 역할을 수행하는 서버.

## ws 의 기능
1.빠르다
2.리버스 프록시로 사용가능
3.ssl지원
4.웹페이지 접근인증
5.압축
6.비동기처리

### 리버스 포록시
1. 로드 벨런싱에 사용
2. 본래 서버의 ip주소 노출 안시킴 ,보안 유리
3. 캐시 데이터 저장

### ssl
보안처리가 잘 되어있는 것을 인증해주는것 
nginx가 https를 쓰면 ssl로 인해 쉽게 쓸수있음

### 로드 밸런싱
로드 밸런싱이란 말 그대로 서버가 처리해야 할 업무 혹은 요청(Load)을 여러 대의 서버로 나누어(Balancing) 처리하는 것을 의미한다. 
한 대의 서버로 부하가 집중되지 않도록 트래픽을 관리해 각각의 서버가 최적의 퍼포먼스를 보일 수 있도록 하는 것이 목적이다.

## ws 의 종류
1. Nginx
2. Tomcat
3. Caddy

## WAS만쓰지 않고 별도로 WS를 쓰는이유
WAS의 부담을 줄여주기 위하여

### WS가 WAS 앞단에 있으면 좋은 이유
WAS도 보통 자체적으로 웹 서버 기능을 내장하고 있다. WAS의 초창기에는 WAS의 성능이 부실하여 WS와 같이 썼지만 지금은 WAS만으로 충분하다.
그럼에도 WS가 WAS 앞단에 있으면 좋은 이유는 기능을 분리하여 서버 부하를 방지하기 위해서이다.
WS는 단순한 문지기 역할을 하면서 여러개의 WAS(java서버, C서버, phython서버)를 WS에서 연결해줄 수 있다.
그리고 단순한 정적 페이지는 WAS대신 WS가 반환하는게 자원이 적게 든다.
또 무중단으로 운영하기 위해 중요한 기능이라고 한다.

