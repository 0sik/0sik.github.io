---
layout: single
title: "RESTful, HTTPS, TCP,UDP"
toc: true
toc_sticky: true
toc_label: "목차"
categories: backendstudy
toc_icon: "bars"
tags: [backendstudy]
---

📘 RESTful, HTTPS, TCP,UDP

# RESTful
1. REST의 개념
- HTTP URI를 통해 자원을 명시하고 HTTP Method를 통해 해당 자원에 대한 CRUD작용 하는 것을 의미
2. REST API
- API : 데이터와 기능의 집합을 제공하여 컴퓨터 프로그램간 상호작용을 촉진, 서로 정보를 교환 가능 하도록 함
- REST API : REST기반으로 서비스 API를 구현한 것 
3. RESTful : RESTAPI를 제공하는 웹 서비스

# HTTPS
HTTP : 서버/클라이언트 모델을 따라 데이터를 주고 받기 위한 프로토콜
HTTPS : HTTP에 데이터 암호화가 추가된 프로토콜이다. HTTPS는 HTTP와 다르게 443번 포트를 사용하며, 네트워크 상에서 중간에 제3자가 정보를 볼 수 없도록 암호화를 지원하고 있다.

# TCP ,UDP
TCP는 Transmission Control Protocol의 약자이고, UDP는 User Datagram Protocol의 약자이다. 두 프로토콜은 모두 패킷을 한 컴퓨터에서 다른 컴퓨터로 전달해주는 IP 프로토콜을 기반으로 구현되어 있지만, 서로 다른 특징을 가지고 있다.

## UDP
- 데이터를 데이터그램 단위로 처리하는 프로토콜
- 비연결형 서비스로 데이터그램 방식을 제공한다
- 정보를 주고 받을 때 정보를 보내거나 받는다는 신호절차를 거치지 않는다.
- UDP헤더의 CheckSum 필드를 통해 최소한의 오류만 검출한다.
- 신뢰성이 낮다
- TCP보다 속도가 빠르다

## TCP
- 인터넷상에서 데이터를 메세지의 형태로 보내기 위해 IP와 함께 사용하는 프로토콜
- 연결 지향 방식으로 패킷 교환 방식을 사용한다
- 3-way handshaking과정을 통해 연결을 설정하고 4-way handshaking을 통해 해제한다.
- 흐름 제어 및 혼잡 제어.
- 높은 신뢰성을 보장한다.
- UDP보다 속도가 느리다.    

## UDP to TCP
- UDP에서 TCP로 업그레이드 할 경우 가장 먼저 해야 될 것
    - TCP 3방향 핸드셰이크이다 이것은 송신자와 수신자 사이에 연결이 설정되는 초기 프로세스이다. 
    - 3방향 핸드셰이크가 완료되면 TCP 연결이 설정되고 데이터 전송이 시작될 수 있습니다. TCP는 연결 지향 프로토콜이고 안정적이고 순서화된 데이터 전달을 보장하기 때문에 UDP에서 TCP로 업그레이드할 때 이 연결 설정 프로세스를 구현하는 것이 필수적입니다.
    - 연결 설정을 구현한 후에는 안정적인 데이터 전송, 혼잡 제어, 흐름 제어 및 오류 처리와 같은 다른 TCP 기능 구현 작업을 수행할 수 있습니다. 이러한 기능은 TCP 연결을 통해 전송된 데이터가 안정적이고 올바른 순서로 전달되도록 종합적으로 보장합니다. 이는 UDP의 비연결 특성과의 주요 차이점입니다.