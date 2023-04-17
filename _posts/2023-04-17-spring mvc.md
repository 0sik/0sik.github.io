---
layout: single
title: "spring mvc"
toc: true
toc_sticky: true
toc_label: "목차"
categories: spring
toc_icon: "bars"
tags: [spring]
---

📘 spring mvc

- 모델, 뷰 컨트롤러는 각각의 인터페이스가 정의되어 있어 서로 구현에 의존적이지 않아 약한 결합도로 구성되어 유연하고 확장하기 쉬움

# model1 방식
- jsp만 사용하여 개발하거나 java bean을 포함하여 개발하는 방식을 의미
- jsp에 뷰와 비즈니스 로직이 혼재되어 복잡도가 높음 - 유지보수 어려움

# model2 방식
- model - view -controller로 분리
- 뷰와 비즈니스 로직의 분리로 유지보수성 및 확장 용이

# 프론트 컨트롤러 패턴 (스프링 mvc)
- 클라이언트 요청을 별도의 프론트 컨트롤러에 집중
    - 모든 요청의 공통 부분을 별도(프론트 컨트롤로)로 처리

## 프론트 컨트롤러 패턴 실행 프로세스
- 프론트 컨트롤러 = DispatcherServlet
1. DispatcherServlet이 http 요청을 받음
2. DispatcherServlet은 서브 Controller로 HTTP 요청 위임
3. 서브 Controller는 클라이언트의 요청 처리를 위해 DAO 객체를 호출
4. DAO 객체는 리소스를 엑세스하여 Model 객체를 생성 후 요청 결과 리턴
5. DispatcherServlet 은 처리 결과에 적합한 뷰에 화면 처리 요청
6. 선택된 뷰는 화면에 모델 객체를 가져와 화면 처리
7. HTTP 응답

## 프론트 컨트롤러 패턴
- DispatcherServlet : 프론트 컨트롤러를 담당한다. 클라이언트의 요청을 받아서 Controller에게 클라이언 트의 요청을 전달하고, 리턴 결과값을 View에게 전달하여 알맞은 응답을 생성한다.
- HandlerMapping : URL과 요청 정보를 기준으로 어떤 컨트롤러를 실행할지 결정하는 객체. DispatcherServlet은 하나 이상의 핸들러 매핑을 가질 수 있음. 애노테이션을 이용 할 때에는 mvn:annotation-driven 태그를 설정해야 함

# 웹 어플리케이션 컨텍스트 등록 설정
- ContextLoadListner 클래스
    - 서블릿 컨테이너(Tomcat)에 ContextLoadListner 클래스 등록
    - 서비스 계층 이하의 빈(@Service, @Repository 등)을 등록하기 위한 클래스
- DispatcherServlet 클래스
    - 서블릿 컨테이너(Tomcat)에 프론트 컨트롤러인 DispatcherServlet 클래스 등록
    - 컨트롤러(@Controller 또는 @Component) 빈을 등록하기 위한 클래스

순서 : 톰캣실행 종료 시점과 wac실행 종료 시점 같음

listener(특정 이벤트 발생 시 실행)을 통해 실행시 초기 설정 가능

root-context.xml(서비스 이하 계층 빈 등록): component-scan 으로 빈 등록 (서비스 이하 di 등록) (서블릿 관련 빈 외 모든 계층 빈 등록)

servlet-context.xml(프론트 컨트롤러 등록) (contextLoadListener상속 받은, 컨트롤러 빈 등록) : component-scan 으로 빈등록 ( 컨트롤러 빈 di 등록) (서블릿관련 계층 빈 등록) annotation-driven을 통하여 등록

# 매핑 설정 방식

1. url경로 내의 변수 값을 @PathVariable 적용 변수로 전달
    - @RequestMapping(value="/try/{msg}", method = RequestMethod.GET)
public String getUserTest( @PathVariable("msg") String msg)

2. 요청 파라미터 값을 @RequestParam적용 변수로 전달
    - @RequestMapping(value="/tryA", method = RequestMethod.GET)
public String getUserTest1( @RequestParam("msg") String msg ) 

3. 요청 파라미터 값을 @ModelAttribute적용 변수로 전달
    - @RequestMapping(value="/tryB", method = RequestMethod.GET)
public String getUserTest2( @ModelAttribute("msg") String msg )

4. @RequestMapping(value={"/tryC", "/tryD"})
• 배열 형태의 값을 지정할 수 있음
• tryC, tryD 양쪽 URL에 대응하는 메서드를 정의할 수 있음
- 요청 파라미터 값을 @ModelAttribute 적용 변수로 전달

    - @RequestMapping(value={"/tryC", "/tryD"}, method = RequestMethod.GET)
public String getUserTest2( @ModelAttribute("msg") String msg ) 