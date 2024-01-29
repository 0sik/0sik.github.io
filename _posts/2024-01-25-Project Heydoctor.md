---
layout: single
title: "병원 예약, 챗봇 서비스(HeyDoctor)"
toc: true
toc_sticky: true
toc_label: "목차"
categories: project
toc_icon: "bars"
tags: [project]
---
📘 병원 예약, 챗봇 서비스(HeyDoctor)

한국공학대학교 Graduation Project이다. AI 챗봇을 이용한 건강 자가진단 및 주변 병원 온라인 예약 서비스인데, AI챗봇서버는 Docker을 활용하여 Flask서버이고, 카카오톡 디벨로퍼의 카카오톡이 되게 하였고, 카카오톡에서 요청이오면 챗봇 서버로 요청이 가게 설계했다.
그리고 자기 자신 주변 병원 위치나 운영시간 등등을 알수있는 웹사이트 하나 만들었다.

이 프로젝트에서는 인프라쪽을 대부분을 맡아서 진행하였다. 

CICD나 HTTPS같은 기본 개념적인거를 정리하기 보다 내가 인프라를 설계하면서 얻은 이점같은것들을 정리해보자

# NGINX을 이용하여 단일서버 이용
Nginx를 사용하여 단일 서버에 백엔드와 프런트엔드를 모두 배포하면 배포 및 유지 관리가 어느 정도 단순화될 수 있으며, 특히 소규모 프로젝트에서 비용을 절감하는 데 도움이 될 수 있다. Nginx는 역방향 프록시 역할을 하여 요청을 적절한 백엔드(서버 측) 또는 프론트엔드(클라이언트 측) 구성 요소로 전달할 수 있다.

아무래도 3명이서 하는 프로젝트다 보니 배포 역할을 한명이 담당해야 했는데 그러다보니 단일 서버만 이용할수밖에없었다.
그래서 nginx을 이용하여 단일서버에 프론트 백 데이터베이스까지 docker compose를 이용하여 비용을 감소하였다.

하지만 이러한 방법은 안좋을수 있다.
확장성이 제약될수있고, 프론트 백이 격리되지 않아 문제가 발생하면 다른 구성에 영향을 미칠 수 있다.


# Docker compose 를 이용하여 데이터베이스 비용 감소
데이터베이스(MYSQL)도 docker compose 를 이용하여 따로 RDS를 이용하지 않고 데이터 베이스를 사용하였다 .

Docker Compose를 사용하여 MySQL 데이터베이스 컨테이너를 관리하면 AWS의 RDS(관계형 데이터베이스 서비스)와 같은 다른 호스팅 솔루션에 비해 잠재적인 비용 절감이나 EC2(Elastic Compute Cloud) 인스턴스에서 전용 MySQL 인스턴스를 관리하는 등 다양한 이점을 제공할 수 있다.



비용적인 측면에서는 분명 nginx와 docker compose를 이용한 데이터베이스의 비용이 감소된다.
하지만 과연 실전에서 특히 회사에서는 이렇게 단일 서버를 이용할까?

# 예전 프로젝트 피드백
예전에 큐시즘이라는 동아리를 하였었다. 그때 Prometheus 와 Grafana 를 docker compose 로 백엔드 서버에 같이 올리게 된적이 있었다.
그때 현직 개발자가 우리것을 평가하였는데 그때 이것에 대해 물어봤었다. 그렇게 한 이유가 있냐고, 

Prometheus와 Grafana 모두 상당한 리소스를 소비할 수 있다. 특히 Prometheus에서 스크랩하는 측정항목이 많거나 Grafana에서 대량의 데이터 시각화를 처리하는 경우 더욱 그렇다. 동일한 서버에서 실행하면 리소스 경합이 발생하고 두 응용 프로그램의 성능에 영향을 미칠 수 있다.
트래픽이 많거나 모니터링할 지표가 많은 프로덕션 환경에서는 Prometheus와 Grafana를 별도의 서버나 별도의 클러스터에 배포하는 것이 더 바람직할 수 있다.
동일한 서버에서 Prometheus와 Grafana를 모두 실행하면 초기 설정이 단순화될 수 있지만 유지 관리 및 업그레이드가 복잡해질 수 있다. 한 구성 요소에 업데이트나 변경이 필요한 경우 실수로 다른 구성 요소에 영향을 미쳐 호환성 문제가 발생할 수 있다.

하지만 우리는 짧게하는 프로젝트이기도 하고, 상당히 많은 트래픽을 다루지 않기 때문에 비용적으로 생각해서 단일 서버에 올렸다고 말한적이 있다.

이번에 블로그에 쓴것과 같은 내용인거 같다.

확실히 단일서버에 올리면 유지보수 업그레이드, 격리 확장성등이 단점이 될순 있겠지만 
작은 프로젝트인만큼 비용적으로 이점을 볼 수 있는거 같다.