---
layout: single
title: "Spring Mybatis"
toc: true
toc_sticky: true
toc_label: "목차"
categories: spring
toc_icon: "bars"
tags: [spring]
---

📘 Spring Mybatis

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

## 쓰는법

1. Mapper.xml에 sql문을 등록한다.
2. @Autowired private SqlSession sqlSession;
3. public StudentVO read(String id) throws Exception 
StudentVO vo = sqlSession.selectOne(namespace+".selectByid", id);
return vo;