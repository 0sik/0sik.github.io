---
layout: single
title: "REST API"
toc: true
toc_sticky: true
toc_label: "목차"
categories: network
toc_icon: "bars"
tags: [network]
---

📘REST API
# API란

API란 클라이언트가 리소스를 요청할 수 있도록 서버측에서 제공된 인터페이스(interface)를 말한다.

# REST API

REST 기반으로 서비스 API를 구현하는 것

REST API는 HTTP 요청을 통해 통신하여 데이터 생성, 읽기, 업데이트 및 삭제 기능을 완료합니다. CRUD 작업이라고도 합니다. REST는 요청된 리소스에 대한 정보를 제공하고 리소스로 수행할 작업을 설명하는 네 가지 방법을 사용합니다.

POST — 리소스 생성

GET — 리소스 가져오기

PUT — 리소스 업데이트

DELETE — 리소스를 삭제합니다.

## 규칙
1) URI는 정보의 자원을 표현해야 한다. (리소스명은 동사보다는 명사를 사용) 명사는 복수형
    GET /members/delete/1 (x)
위와 같은 방식은 REST를 제대로 적용하지 않은 URI입니다. URI는 자원을 표현하는데 중점을 두어야 합니다. delete와 같은 행위에 대한 표현이 들어가서는 안됩니다.

2) 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE 등)로 표현
위의 잘못 된 URI를 HTTP Method를 통해 수정해 보면

    DELETE /members/1
으로 수정할 수 있겠습니다.
회원정보를 가져올 때는 GET, 회원 추가 시의 행위를 표현하고자 할 때는 POST METHOD를 사용하여 표현합니다.

회원정보를 가져오는 URI

    GET /members/show/1     (x)
    GET /members/1          (o)
회원을 추가할 때

    GET /members/insert/2 (x)  - GET 메서드는 리소스 생성에 맞지 않습니다.
    POST /members/2       (o)

RESTFUL이란 REST의 원리를 따르는 시스템을 의미합니다. 하지만 REST를 사용했다 하여 모두가 RESTful 한 것은 아닙니다.  REST API의 설계 규칙을 올바르게 지킨 시스템을 RESTful하다 말할 수 있으며

모든 CRUD 기능을 POST로 처리 하는 API 혹은 URI 규칙을 올바르게 지키지 않은 API는 REST API의 설계 규칙을 올바르게 지키지 못한 시스템은 REST API를 사용하였지만 RESTful 하지 못한 시스템이라고 할 수 있습니다