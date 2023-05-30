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
3. pointcut : A란 메서드의 진입 시점에 호출할것 과 같이 더욱 구체적으로 advice가 실행될 지점을 정할수 있음
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

> 코드설명 : 포인트컷 표현식 excution(*read(String))은 이 어드바이스가 read(String)서명이 있는 모든 메서드에 적용된다
메서드가 실행되기 전에 호출되고 있음을 나타내는 메시지를 인쇄합니다. JoinPoint#getSignature()를 사용하여 메서드 서명을 검색하고 메서드 이름을 인쇄합니다. 또한 JoinPoint#getArgs()를 사용하여 메서드 인수를 검색하고 첫 번째 인수의 값을 인쇄합니다.

@AfterReturning 주석은 대상 메서드가 성공적으로 반환된 후 주석이 지정된 메서드(afterReturningMethod())가 실행됨을 나타냅니다. pointcut 식과 returning 속성은 대상 메서드의 반환 값을 캡처하는 데 사용됩니다.
afterReturningMethod() 메소드 내부에 어드바이스 로직이 구현되어 있습니다. 실행 후 메서드가 호출되었음을 나타내는 메시지를 인쇄합니다. beforeMethod()와 유사하게 메소드 서명과 인수를 검색하고 인쇄합니다.

@AfterThrowing 주석은 대상 메서드가 예외를 throw하는 경우 주석이 지정된 메서드(afterThrowingMethod())가 실행됨을 나타냅니다. 포인트컷 표현식과 throwing 속성은 발생한 예외를 캡처하는 데 사용됩니다.
afterThrowingMethod() 메소드 내부에 어드바이스 로직이 구현되어 있습니다. 메서드에서 예외가 발생했음을 나타내는 메시지를 인쇄합니다. 또한 제공된 Throwable 개체를 사용하여 예외 세부 정보를 인쇄합니다.

 이 aspect 클래스는 "org.tukorea.myweb" 패키지의 read(String) 메서드에 대한 메서드 호출을 가로채고 성공적인 반환 전, 후, 후 또는 대상 메서드에서 예외를 throw한 후 추가 동작을 제공합니다