---
layout: single
title: "RDBMS"
toc: true
toc_sticky: true
toc_label: "목차"
categories: backendstudy
toc_icon: "bars"
tags: [backendstudy]
---

📘Spring Data JPA vs MyBatis

JPA란 자바 진영에서 ORM기술 표준으로 사용되는 인터페이스의 모음이다. 실제적으로 구현된것이 아니라 구현된 클래스와 매핑을 해주기 위해 사용되는 프레임 워크이다 .
먼저 ORM이 뭔지 알아보자

# ORM (Object-Relational Mapping)
애플리케이션 class와 RDB의 테이블을 매핑한다는 뜻이며, 어플리케이션의 객체를 RDB테이블에 자동으로 영속화해주는 것이다.

## ORM의 장점
1. SQL문이 아닌 Method를 통해 DB를 조작할 수 있어, 개발자는 객체 모델을 이용하여 비즈니스 로직을 구성하는데만 집중할 수 있음.
(내부적으로는 쿼리를 생성하여 DB를 조작함. 하지만 개발자가 이를 신경 쓰지 않아도됨)
2. Query와 같이 필요한 선언문, 할당 등의 부수적인 코드가 줄어들어, 각종 객체에 대한 코드를 별도로 작성하여 코드의 가독성을 높임
3. 객체지향적인 코드 작성이 가능하다. 오직 객체지향적 접근만 고려하면 되기 때문에 생산성 증가
4. 매핑하는 정보가 Class로 명시 되었기 때문에 ERD를 보는 의존도를 낮출 수 있고 유지보수 및 리팩토링에 유리
5. 기존 방식에서 MySQL 데이터베이스를 사용하다가 PostgreSQL로 변환한다고 가정해보면, 새로 쿼리를 짜야하는 경우가 생김. 이런 경우에 ORM을 사용한다면 쿼리를 수정할 필요가 없음

## ORM의 단점
1. 프로젝트의 규모가 크고 복잡하여 설계가 잘못된 경우, 속도 저하 및 일관성을 무너뜨리는 문제점이 생길 수 있음
2. 복잡하고 무거운 Query는 속도를 위해 별도의 튜닝이 필요하기 때문에 결국 SQL문을 써야할 수도 있음

# JPA
- Java 진영에서 ORM기술 표준으로 사용하는 인터페이스 모음
- 자바 어플리케이션에서 관계형 데이터베이스를 사용하는 방식을 정의한 인터페이스
- 인터페이스 이기 때문에 Hibernate,OpenJPA등이 JPA를 구현함

## JPA 장점
1. 쿼리를 하나하나 작성할 필요가 없어 코드량이 줄어든다
2. 가독성이좋다.
3. 간편하게 수정이 가능하다 (유지보수, 리팩토링 용이)
4. 동일한 쿼리에 대한 캐시 기능을 사용하기 때문에 더욱 높은 성능을 낼수 있다.

## JPA 단점
1. 매핑 설계를 잘못했을 때 성능 저하가 발생할 수 있다.
2. JPA를 제대로 사용하려면 알아야할 것이 많아서 학습하는데 시간이 오래 걸린다.
3. 다수의 테이블 조인시 신경써야 할게 많다.

# MYBatis
- 객체 지향 언어인 자바의 관계형 데이터베이스 프로그래밍을 좀 더 쉽게 할 수 있게 도와 주는 개발 프레임 워크
- JDBC를 통해 데이터베이스에 엑세스하는 작업을 캡슐화하고 일반 SQL 쿼리, 저장 프로 시저 및 고급 매핑을 지원하며 모든 JDBC 코드 및 매개 변수의 중복작업을 제거 
- Mybatis에서는 프로그램에 있는 SQL쿼리들을 한 구성파일에 구성하여 프로그램 코드와 SQL을 분리할 수 있는 장점을 가지고 있음


## MYBatis특징
- 복잡한 쿼리나 다이나믹한 쿼리에 강함
- 비슷한 쿼리는 남발하게 되는 단점
- 프로그램 코드와 sql쿼리의 분리로 코드의 간결성 및 유지보수성 향상
- resultType, resultClass등 Vo를 사용하지 않고 조회결과를 사용자 정의 DTO, MAP 등으로 맵핑하여 사용 할 수 있다
- 빠른 개발이 가능하여 생산성이 향상된다
- SQL실행 결과를 자바 빈즈 또는 Map객체에 매핑해주는 Persistence 솔루션으로 관리한다. SQL을 소스 코드가 아닌 XML로 분리한다
- SQL문과 프로그래밍 코드를 분리해서 구현한다
- 데이터 소스 기능과 트랜잭션 처리 기능을 제공한다

## MyBatis 장점
1. 접근이 쉽고 코드가 간결
2. SQL문과 프로그래밍 코드가 분리되어 있어서 SQL문에 변경이 있을때마다 자바 코드를 수정하거나 컴파일 하지 않아도 된다.
3. 다양한 프로그래밍 언어로 구현이 가능하다 

## MyBatis단점 
1. 스키마 변경시 SQL쿼리를 직접 수정해주어야 한다
2. 반복된 쿼리가 발생하여 반복 작업이 있다.
3. 쿼리를 직접 작성하기 때문에 데이터베이스에 종속된 쿼리문이 발생할 수 있다.
4. 데이터베이스 변경시 로직도 함께 수정해주어야 한다

# JPA vs MyBatis
JPA는 객체 중심의 개발 방식을 지원하며, 개발자가 작업 SQL을 작성하지 않고도 객체를 관리할 수 있따는 장점이 있고, Mybatis는 SQL을 직접 작성할 수 있어 개발자가 더욱 자유롭게 데이터베이스를 다룰 수 있다는 장점이 있다.