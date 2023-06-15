---
layout: single
title: "spring 특징2"
toc: true
toc_sticky: true
toc_label: "목차"
categories: spring
toc_icon: "bars"
tags: [spring]
---

📘 spring 특징2

## 마이바티스

- 스프링 프레임워크랑 마이바티스 프레임워크 빈 의존관계 설정정보를 설명
    1. 커넥션 풀 지원하는 DataSource빈 등록
    2. 스프링의 트랜잭션 관리자 빈 등록
    3. 마이바티스의 sqlSessionFactory 빈 등록
    4. Mybatis-spring의 sqlSessionTemplate 빈 등록해서 의존관계 성립한다.

- SQL 삽입 값의 연계 방법
    1. 파라미터가 자바 빈즈 객체일 경우
        
        sqlSession.insert(namespace+”.insert”,vo);
        
        <insert id = “insert”>
        
        insert into student(id,passwd) values(#{id},#{passwd})
        
        </insert>
        
    2. 파라미터가 하나이고, 기본 자료형이나 문자일 경우 값을 그대로 전달
        
        StudentVO vo = sqlsession.selectOne(namespace+”selectByid”,id);
        
        <select id = “selectByid” resultType=”org.tukorea.myweb.domain.StudentVO”>
        
        select*from student where id = #{id}
        
        </select>
        
    3. 파라미터가 Map일 경우 #{num}은 Map객체의 키 값이 ‘num’인값을 찾는다
    
    <![CDATA[select*from student]]> 안에있는 특수문자 전부 문자로 받는 CDATA
    
- dao객체하고 메퍼파일의 sql하고 어떻게 연동 하는지 설명
    
    sql실행 결과와 반환값이 되는 객체 간 매핑은 마이바티스에 의해 자동으로 이루어짐
    
- aop정의
    
    관점지향 프로그래밍이다. 횡단 관심사를 중심를 분리하여 설계,객체지향 프로그래밍보다 완성도 높인 프로그래밍 패러다임
    
- aop하고 di의 구현 목적 차이점
    
    di : 의존 관계 빈들의 결합도 낮추기
    
    aop: 횡단관심사 객체와 이에 영향받는 객체의 결합도 낮추기
    
- advice,joinpoint,pointcut 관심사,횡단관심사, 횡단관심사분리, 관점지향프로그래밍 용어 설명
    
    advice : 횡단관심사 구현 부분
    
    joinpoint: advice적용 가능한 지점들
    
    pointcut : 수많은 joinpoint중에서 실제 적용될 지점들
    
    aspect : 공통 관심사의 추상적 명칭
    
    target : 횡단 관심사를 적용 받게 되는 대상으로 어드바이스가 적용되는 객체
    
    weaving : proxy객체를 만드는 과정
    
    proxy : advice가 적용되었을때 만들어지는 객체
    
    관심사 : 애플리케이션 개발 위한 구현 기능들
    
    횡단 관심사 : 여러 모듈에 걸쳐 공통적으로 반복적으로 필요로 하는 처리 내용
    
    횡단 관심사 분리 : 횡단관심사를 한곳으로 모는것
    
    관점지향 프로그래밍 : 횡단 관심사 분리를 실현하는것
    
- advice유형 차이점을 비교
    
    before: 조인포인트 앞에서 실행할  어드바이스 
    
    after: 조인포인트 뒤에서 실행할 어드바이스
    
    after returning  : 조인포인트가 완전히 종료된 다음에 실행되는 어드바이스
    
    around : 조인포인트 앞뒤에서 실행되는 어드바이스
    
    after throwing : 조인포인트에서 예외가 발생했을때 실행되는 어드바이스
    
- proxy 패턴 적용한 내용 이해
    
    직접 참조가 아닌 그 객체를 대행 하는 객체를 통해 대상 객체에 접근하는 방식 , 스프링 컨테이너 초기화 과정에서 스프링 빈 객체 대항할 프록시 객체 생성, 객체 핵심 코드에 대한 영향없이 객체의 접근 전/후 에 대한 중요 처리 가능
    

- **기본원칙 4가지 ACID**
ACID
    - 원자성(Atomicity)
        - 한 트랜잭션 내 모든 연산들이 완전히 수행되거나 전혀 수행되지 않음
    - 일관성(Consistency)
        - 어떤 트랜잭션 수행되기 전 DB가 일관된 상태를 가졌다면 트랜잭션 수행 후에도
        또 다른 일관된 상태를 가짐 (제약조건 등)
    - 고립성(Isolation)
        - 한 트랜잭션이 데이터 갱신동안 이 트랜잭션 완료 전까지 다른 트랜잭션에서
        이 데이터에 접근 불가
    - 지속성(Durability)
        - 한 트랜잭션 완료되면 DB에 반영한 수행 결과는 영구적이어야 함

- **aop를 이용한 스프링에서의 트랜잭션 방식을 설명하시오**
    
    AOP로 서비스에 트랜잭션 처리를 구현한 어드바이스 적용함으로써
    서비스 내부 수정하지 않고 트랜잭션을 처리, 트랜잭션 처리는 트랜잭션 관리자, 트랜잭션 어드바이스 사용
    
- **스프링부트 특징**
    
    **독립 실행형 앱을 제공한다, was가 내장돼있다,**  의존 관계 라이브러리 조합 제공
    
    - Spring Boot Starter : 미리 정의한 의존 관계 라이브러리 조합 제공
    - spring-boot-starter-web : 하나의 의존 관계를 추가
    -> Spring MVC, Tomcat, 웹 애플리케이션에 필요한 라이브러리가 함께 추가
    - Spring Boot Starter Parent
        - 라이브러리 버전 간 충돌 및 호환 문제 발생 가능
        -> 검증된 의존 관계 라이브러리 조합 제공
        
- **스프링부트어플리케이션 의미**
    
    @SpringBootApplication
    = @SpringBootConfiguration + @ComponentScan + @EnableAutoConfiguration
    
    - @SpringBootConfiguration : @Configuration 같은 의미
    - @ComponentScan : 명시한 클래스 찾아 스프링 빈으로 등록
    - @EnableAutoConfiguration : 사전에 정의한 라이브러리들을 대상으로 조건이 만족 될	경우 빈으로 등록해 주는 애노테이션
    

- **인터셉터하고 필터의 차이점**
    
    인터셉터는 스프링 컨텍스트내에 존재해서 스프링 컨텍스트내에 접근가능 디스패처서블릿 후에 실행 필터는 웹 애플리케이셔내에서 동작해서 스프링 context접근 어려움 디스패처서블릿 전에 실행
    

- **인터셉터하고 aop의 차이점**
    
    - 인터셉터의 파라미터가 HttpServletRequest, HttpServletResponse 임
    
    - aop는 JoinPoint, PreceedingJoinPoint 등의 파라미터 활용하는 방식
    
    

- **위에 통해서 동작방식(구조) 설명(컴포턴트 등)**
    
    Authentication Filter을 통해 Manager에서 인증처리를 수행하고 Provider에서 인증처리 기능을 수행한다.
