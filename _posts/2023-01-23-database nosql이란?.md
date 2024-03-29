---
layout: single
title: "nosql이란?"
toc: true
toc_sticky: true
toc_label: "목차"
categories: database
toc_icon: "bars"
tags: [database]
---

📘nosql

# nosql이란

NoSQL 데이터베이스(일명 "SQL만을 사용하지 않는 데이터베이스")는 표 형식이 아니며, 관계형 테이블과는 다른 방식으로 데이터를 저장합니다. NoSQL 데이터베이스는 데이터 모델에 따라 유형이 다양합니다. 주요 유형으로는 문서, 키 값, 와이드 컬럼, 그래프가 있습니다. 이들은 유연한 스키마를 제공하며, 대량의 데이터와 높은 사용자 부하에서도 손쉽게 확장이 가능합니다.

## nosql의 특징
1. RDBMS와 달리 데이터 간의 관계를 정의하지 않는다.
RDBMS는 데이터 관계를 외래키 등으로 정의하고 JOIN 연산을 수행할 수 있지만, NoSQL은 JOIN 연산이 불가능하다.

2. RDBMS에 비해 대용량의 데이터를 저장할 수 있다.
페타바이트 급의 대용량 데이터를 저장할 수 있다.

3. 분산형 구조이다.
여러 곳의 서버에 데이터를 분산 저장해 특정 서버에 장애가 발생했을 때도 데이터 유실 혹은 서비스 중지가 발생하지 않도록 한다.

4. 고정되지 않은 테이블 스키마를 갖는다.
RDBMS와 달리 테이블의 스키마가 유동적이다. 데이터를 저장하는 칼럼이 각기 다른 이름과 다른 데이터 타입을 갖는 것이 허용된다.

## nosql의 장점 
1. 데이터의 구조가 거의 또는 전혀 없는 대용량의 데이터를 저장하는 경우
대부분의 NoSQL 데이터베이스는 저장할 수 있는 데이터의 유형에 제한이 없다.
필요에 따라, 언제든지 데이터의 새 유형을 추가할 수 있다.
소프트웨어 개발에 정형화 되지 않은 많은 양의 데이터가 필요한 경우, NoSQL을 적용하는 것이 더 효율적일 수 있다.

2. 빠르게 서비스를 구축하는 과정에서 데이터 구조를 자주 업데이트 하는 경우
NoSQL 데이터베이스의 경우 스키마를 미리 준비할 필요가 없기 때문에 빠르게 개발하는 과정에 매우 유리하다.
시장에 빠르게 프로토타입을 출시해야 하는 경우가 이에 해당한다.
또한 소프트웨어 버전별로 많은 다운타임(데이터베이스 서버를 오프라인으로 전환하여 데이터 처리를 진행하는 작업 시간) 없이 데이터 구조를 자주 업데이트 해야하는 경우, 스키마를 매번 수정해야 하는 관계형 데이터베이스 보다 NoSQL 기반의 비관계형 데이터베이스를 사용하는 게 더 적합하다.

3. 비정형 데이터 구조 설계로 설계 비용 감소

## nosql 의 종류

1. Key-Value Database

기본적인 패턴으로 KEY-VALUE 하나의 묶음(Unique)으로 저장되는 구조로 단순한 구조이기에 속도가 빠르며 분산 저장 시 용이하다.

Key 안에 (COLUMN, VALUE) 형태로 된 여러 개의 필드, 즉 COLUMN FAMILIES 갖는다.

Ex) Redis, Oracle NoSQL Database, VoldeMorte

2. Wide-Column Database

행마다 키와 해당 값을 저장할 때마다 각각 다른값의 다른 수의 스키마를 가질 수 있다.

사용자의 이름(key)에 해당하는 값에 스키마들이 각각 다름을 볼 수 있다.

이러한 구조를 갖는 WIDE COLUMN DATABASE 는 대량의 데이터의 압축, 분산처리, 집계 쿼리 (SUM, COUNT, AVG 등)및 쿼리 동작 속도 그리고 확장성이 뛰어난 것이 그 대표적 특징이라 할 수 있다.

EX) Hbase, GoogleBigTable, Vertica

3. Document Database

테이블의 스키마가 유동적, 즉 레코드마다 각각 다른 스키마를 가질 수 있다.

보통 XML, JSON과 같은 DOCUMENT를 이용해 레코드를 저장한다.

트리형 구조로 레코드를 저장하거나 검색하는 데 효과적이다.

Ex) MongoDB, CouchDB, Azure Cosmos DB

4. Graph Database

데이터를 노드로(그림에서 파란, 녹색 원) 표현하며 노드 사이의 관계를 엣지(그림에서 화살표)로 표현

일반적으로 RDBMS 보다 성능이 좋고 유연하며 유지보수에 용이한 것이 특징.

Social networks, Network diagrams 등에 사용할 수 있다.


Ex) Neo4j, BlazeGraph, OrientDB