---
layout: single
title: "인메모리 데이터베이스 REDIS"
toc: true
toc_sticky: true
toc_label: "목차"
categories: database
toc_icon: "bars"
tags: [database]
---

📘redis

# redis란
Key, Value구조의 비정형 데이터를 저장하고 관리하기 위한 오픈 소스 기반의 비관계형 데이터 베이스 관리 시스템 ,
데이터베이스 ,캐시 ,메세지 브로커로 사용되며 인 메모리 데이터 구를 가진 저장소 입니다.

## redis의 인메모리 구조
    - 사용자가 늘어난다면 데이터 베이스 과부 될수 있기 때문 이때 캐시 서버 도입 하여 사용 
    데이터 베이스는 데이터를 물리 디스크에 직접 쓰기 때문에 서버에 문제가 발생하여 다운되더라도 데이터가 손실되지 않습니다.
    하지만 매번 디스크에 접근해야 하기 때문에 사용자가 많아질수록 부하가 많아져서 느려질 수 있습니다.
    캐시는 한번 읽어온 데이터를 임의의 공간에 저장하여 다음에 읽을 때는 빠르게 결괏값을 받을 수 있도록 도와주는 공간입니다.
    같은 요청이 여러 번 들어오는 경우 매번 데이터 베이스를 거치는 것이 아니라 캐시 서버에서 첫 번째 요청 이후 저장된 결괏값을 바로 내려주기 때문에 DB의 부하를 줄이고
    서비스의 속도도 느려지지 않는 장점이 있습니다.

## redis의 특징 
1. 데이터를 디스크에 쓰는 구조가 아니라 메모리에서 데이터를 처리하기 때:문에 속도가 빠릅니다
2. Single Threaded이다
   - 한 번에 하나의 명령만 처리할 수 있습니다. 그렇게 때문에 중간에 처리 시간이 긴 명렁어가 들어오면 그 뒤에 명령어은 모두 앞에 있는 명렁어가 처리될 때 까지
     대기가 필요합니다.
3. 서버에 장애가 발생했을 경우 그에 대한 운영 플랜이 필요합니다
  - 인모메리 데이터 저장소의 특성상, 서버에 장애가 발생했 경우 데이터 유실이 발생할 수 있기 때문입니다.

## redis의 쓰임
1. 인메모리 데이터베이스
2. 캐시
3. 메세지 브로커(성능이좋지않음)

### 메세지 브로커로 쓰이는 redis

## 도커에서 redis cli환경
도커에서 터미널을 이용해 redis cli환경으로 이동하는 함수 
> redis-cli

cli환경으로 이동

> Keys * 

저장된 키값들이 나옴

> get<Key>

해당 키 값안 데이터 보기

