---
layout: single
title: "메트릭 수집을 통한 모니터링"
toc: true
toc_sticky: true
toc_label: "목차"
categories: monitoring
toc_icon: "bars"
tags: [monitoring]
---

📘모니터링


# Prometheus
메트릭 기반의 오픈소스 모니터링 시스템이다
이벤트 모니터링 및 경고에 사용되는 무료 소프트웨어 용용 프로그램이다.

>  메트릭 : 수집하는 시계열 데이터를 일컫는 말 , 서비스 현황에 대한 정보 , 서버의 상태를 알 수 있는 지표cpu사용량 , 메모리 할당량 , DAU등)

기능 
1. 메트릭 수집, 시계열 데이터 저장(기존의 있던 데이터도 다 저장됨 ex)데이터베이스
2. 그라파나를 이용한 데이터 시각화
3. alertmanager를 통한 알림
4. 서버 지연 시간을 모아둠(시장의 표준)

> QPS : Quries-per-second : 초당 처리 할 수 있는 쿼리 수

> UPS : User-per-second

> SLO : Service Level Objective -> 사용자의 최대 로딩 시간 규정

## node exporter
exporter 는 Prometheus 가 pull 방식으로 데이터를 수집할 수 있도록 메트릭을 노출하는 agent 이다

이 exporter 가 서버들로부터 메트릭을 수집해 /metrics HTTP endpoint 를 제공한다. 그러면 Prometheus 는 exporter 가 열어놓은 HTTP endpoint 로 GET 요청을 날려 메트릭을 수집한다.(Pull 방식)

고로 이 방식이 가능하게 하기 위해선 우리가 모니터링을 할 서버에 exporter 가 설치되어 있어야 한다.
exporter 중 하나는 Node exporter 이다.

Node exporter 는 Cpu, Memory, Disk 등과 같은 다양한 하드웨어 상태와 커널 관련 정보들을 메트릭으로 수집하고 api 로 제공한다.

예를 들어 AWS ec2 instance 에 Node exporter 가 설치되어있다면 Prometheus 는 해당 ec2 에 접근해 위와 같은 정보들을 수집할 수 있게 된다.

## CAdvisor
cAdiviosor는 컨테이너 기반의 모니터링 메트릭을 수집하는 exporter이다
그룹에 관한 메트릭을 제공한다. 
모든 컨테이너의 cpu와 메모리,file,network사용량 등 system metrics정보를 수집하고 그 외에 시스템 이벤트도 모니터링한다. 

# Grafana

시계열 매트릭 데이터를 시각화 하는데 가장 최적화된 대시보드를 제공해주는 오픈소스 툴킷이다
지원되는 데이터 소스에 연결될 때 웹의 차트, 그래프, 경보를 제공한다
성능 관점에서 분석할 수 있다.
대시보드를 통해 인터렉티브한 시각화 기능을 제공하고, Prometheus, InfluxDB, Elasticsearch등 다양한 데이터 소스와 연동할 수 있다

Grafana는 시계열 메트릭 데이터 수집에 최적화 되있으며, 보통 서버 리소스의 메트릭 정보나 로그 같은 데이터를 시각화할때 많이 사용한다