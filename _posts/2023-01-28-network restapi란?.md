---
layout: single
title: "RESTAPI"
toc: true
toc_sticky: true
toc_label: "목차"
categories: network
toc_icon: "bars"
tags: [network]
---

📘RESTAPI


REST API는 HTTP 요청을 통해 통신하여 데이터 생성, 읽기, 업데이트 및 삭제 기능을 완료합니다. CRUD 작업이라고도 합니다. REST는 요청된 리소스에 대한 정보를 제공하고 리소스로 수행할 작업을 설명하는 네 가지 방법을 사용합니다.

POST — 리소스 생성

GET — 리소스 가져오기

PUT — 리소스 업데이트

DELETE — 리소스를 삭제합니다.


RESTFUL이란 REST의 원리를 따르는 시스템을 의미합니다. 하지만 REST를 사용했다 하여 모두가 RESTful 한 것은 아닙니다.  REST API의 설계 규칙을 올바르게 지킨 시스템을 RESTful하다 말할 수 있으며

모든 CRUD 기능을 POST로 처리 하는 API 혹은 URI 규칙을 올바르게 지키지 않은 API는 REST API의 설계 규칙을 올바르게 지키지 못한 시스템은 REST API를 사용하였지만 RESTful 하지 못한 시스템이라고 할 수 있습니다