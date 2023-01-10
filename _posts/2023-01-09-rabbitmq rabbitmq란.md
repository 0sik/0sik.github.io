---
layout: single
title: "rabbitmq란?"
toc: true
toc_sticky: true
toc_label: "목차"
categories: rabbitmq
toc_icon: "bars"
tags: [rabbitmq]
---

📘rabbitmq

# Message broker
Message broker는 송신자의 이전 메시지 프로토콜로부터의 메시지를 수신자의 이전 메시지 프로토콜로 변환하는 중간 모듈이다. 
Kafka, ActiveMQ, OpenMessage Queue, RabbitMQ, Redis등이 여기에 해당된다.

장고에서 발생한 요청을 message broker가 받아 celery를 이용하여 분산처리한다

## messagebroker 종류
1. rabbitmq
2. kafka
3. Redis


# Rabbitmq가 하는일
1. MOM (Message Oriented Middleware): 메시지 미들웨어의 이론, 개념, 설계도를 의미

2. Message Queue: 단순히 자료구조로써는 메시지들을 큐 형태로 다루는 구조를 의미
하지만 거의 더 나아가 MOM의 단순 구현체의 개념으로 사용하는 경우가 더 많은 것 같습니다. '애플리케이션 간의 메시지 큐를 통한 단순한 형태의 통신 솔루션'으로 말이죠.
다시 말해서, 메시지 전송을 위해 메시지 큐, 메시지 전송 구조를 가진 미들웨어로 볼 수 있습니다.

3. Message Broker: 메시지 브로커는 메시지 큐에서 더 확장된 기능을 가지고 있다고 봅니다. 
더 광범위한 전송, 메시지 내용을 통한 라우팅 및 추가/고급 기능 등을 지원하고, 구현체 별로 어떤 방식을 통해 메시지를 전달하고,
내부 구조를 어떻게 구현했는가에 따라 동작하는 방식, 목적, 성능이 달라집니다.


## Rabbitmq의 장점

1. 비동기 : 메시지 큐 생산된 메시지의 저장, 전송에 대해 동기화 처리를 진행하지 않고, 큐에 넣어 두기 때문에 나중에 처리할 수 있다.
2. 탄력성(Resilience)
   소비자 서비스가 다운되더라도 어플리케이션이 중단되는 것은 아니다. 메시지는 메시지 큐에 남아 있다. 소비자 서비스가 다시 시작될 때마다 
   추가 설정이나 작업을 수행하지 않고도 메시지 처리를 시작할 수 있다.
3. 워커에게 일 지정 : 메시지 큐에 저장된 메시지를 워커(Celey)에게 전달하여 비동기적 처리가 가능, 여러가지 많은 메시지를 비동기적 처리 할 수 있음

