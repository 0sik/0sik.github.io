---
layout: single
title: "spring aop"
toc: true
toc_sticky: true
toc_label: "목차"
categories: spring
toc_icon: "bars"
tags: [spring]
---

📘 spring aop

# 스프링 aop
- AOP는 Aspect Oriented Programming의 약자로 관점 지향 프로그래밍 이라고 부른다.
- 어떤 로직을 기준으로 핵심적인 관점, 부가적인 관점으로 나누어서 보고 그 관점을 기준으로 각각 모듈화 하겠다는 것
    - 모듈화란 어떤 공통된 로직이나 기능을 하나의 단위로 묶는 것을 말함
- 각 관점을 기준으로 로직을 모듈화 한다는 것은 코드들을 부분적으로 나누어서 모듈화 하겠다는 의미
- 소스 코드상에서 다른 부분에 계속 반복해서 쓰는 코드들을 발견할 수 있는데 이것을 흩어진 관심사라 부른다
- 흩어진 관심사를 Aspect로 모듈화 하고 핵심적인 비즈니스 로직에서 분리하여 재사용 하겠다는 것이 AOP의 취지이다.

# 용어 정리 
1. @Aspect : 이 클래스가 관점임을 나타내는 어노테이션
2. JoinPoint : Advice가 적용될 위치, 끼어들 수 있는 지점, 메서드 진입 지점, 생성자 호출 시점, 필드에서 값을 꺼내올때 둥 다양한 시점에 적용가능

# 예시
 
    ```
    
@Aspect
@Component
public class MemberAspect {
	
	   @Before("execution(* read(String))")
	   public void beforeMethod(JoinPoint jp) {
	        System.out.println("[BeforeMethod] : 메소드 호출 전");
	        Signature sig = jp.getSignature();
	        System.out.println(" 메소드 이름:" + sig.getName());
	        Object[] obj = jp.getArgs();
	        System.out.println(" 인수 값:" + obj[0]);
	   }
	    @After("execution(* read(String))")
	    public void afterMethod() {
	        System.out.println("[AfterMethod] : 메소드 호출 후");
	    }
	    @AfterReturning(value = "execution(* read(String))", returning = "member")
	    public void afterReturningMethod(JoinPoint jp, StudentVO member) {
	    	System.out.println("[afterReturningMethod] : 메소드 호출 후");
	        Signature sig = jp.getSignature();
	        System.out.println(" 메소드 이름:" + sig.getName());
	        Object[] obj = jp.getArgs();
	        System.out.println(" 인수 값:" + obj[0]);
	    }

	    @AfterThrowing(value = "execution(* read(String))", throwing = "ex")
	    public void afterThrowingMethod(Throwable ex) {
	        // 메소드 호출이 예외를 내보냈을 때 호출되는 Advice
	        System.out.println("[AfterThrowingMethod] : 예외 발생 후");
	        System.out.println("exception value = " + ex.toString());
	    }
}

    ```

> 코드설명 : 