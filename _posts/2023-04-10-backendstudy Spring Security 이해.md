---
layout: single
title: "Spring Security 이해"
toc: true
toc_sticky: true
toc_label: "목차"
categories: backendstudy
toc_icon: "bars"
tags: [backendstudy]
---

📘 Spring Security 이해 ( Spring Security를 사용한 인증 인가와 그렇지 않은 인증 인가 구현에 대한 차이 이해하기 )

# Spring Security

 - 스프링 시큐리티 (Spring Security)는 스프링 기반 어플리케이션의 보안(인증과 권한, 인가)을 담당하는 스프링 하위 프레임워크

 - 보안과 관련해서 체계적으로 많은 옵션들을 제공해주기 때문에 개발자의 입장에서는 하나하나 보안 관련 로직을 작성하지 않아도 된다는 장점이 있다.

## Spring Security 용어

- 인증(Authentication) : 해당 사용자가 본인인지 확인하는 절차

- 인가(Authorization) : 인증된 사용자가 요청한 자원에 접근 가능한지 결정하는 절차

- 접근 주체(Principal) : 보호받는 Resource에 접근하는 대상

- 비밀번호(Credential) : Resource에 접근하는 대상의 비밀번호

- 권한 : 인증된 주체가 어플리케이션의 동작을 수행할 수 있도록 허락되어 있는지 결정
    - 인증 과정을 통해 주체가 증명된 이후 권한을 부여할 수 있다.
    - 권한 부여에 두 가지 영역이 존재하는데 웹 요청 권한과 메서드 호출 및 도메인 인스턴스에 대한 접근 권한 부여가 있다.

## Spring Security 동작 원리 

Spring Security는 웹 애플리케이션에서 인증(authentication)과 인가(authorization)를 구현하기 위한 프레임워크입니다.

인증은 사용자가 자신이 주장하는 신원을 입증하는 과정입니다. 인가는 인증된 사용자가 어떤 자원(resource)에 접근할 수 있는지를 결정하는 과정입니다.

### 간단 로그인 과정

1. 로그인 시도 -> username, password 정보를 HTTP body로 전달

2. 인증 관리 -> UserDetailsService에게 username을 전달하고 회원 상세정보를 요청

3. 회원 DB에서 회원 조회 -> 조회된 정보를 UserDetails로 변환

4. 인증 관리자가 인증 처리 -> UserDetailsService가 전달해준 UserDetails의 정보와 클라이언트가 시도한 username,password 일치 여부 확인

5. UserDetails의 password는 암호문이기에 클라이언트가 보낸 password를를 암호화 하여 비교

### 상세 로그인 과정
1. 요청 수신
    - 사용자가 form을 통해 로그인 정보가 담긴 Request를 보낸다.

2. 토큰 생성
    - AuthenticationFilter가 요청을 받아서 UsernamePasswordAuthenticationToken토큰(인증용 객체)을 생성
    - UsernamePasswordAuthenticationToken은 해당 요청을 처리할 수 있는 Provider을 찾는데 사용

3. AuthenticationFilter로 부터 인증용 객체를 전달 받는다.
    - Authentication Manager에게 처리 위임
    - Authentication Manager는 List형태로 Provider들을 갖고 있다.

4. Token을 처리할 수 있는 Authentication Provider 선택
    - 실제 인증을 할 AuthenticationProvider에게 인증용 객체를 다시 전달한다.

5. 인증 절차
    - 인증 절차가 시작되면 AuthenticationProvider 인터페이스가 실행되고 DB에 있는 사용자의 정보와 화면에서 입력한 로그인 정보를 비교

6. UserDetailsService의 loadUserByUsername메소드 수행
    - AuthenticationProvider 인터페이스에서는 authenticate() 메소드를 오버라이딩 하게 되는데 이 메소드의 파라미터인 인증용 객체로 화면에서 입력한 로그인 정보를 가져올 수 있다.

7. AuthenticationProvider 인터페이스에서 DB에 있는 사용자의 정보를 가져오려면, UserDetailsService 인터페이스를 사용한다.

8. UserDetailsService 인터페이스는 화면에서 입력한 사용자의 username으로 loadUserByUsername() 메소드를 호출하여 DB에 있는 사용자의 정보를 UserDetails 형으로 가져온다. 만약 사용자가 존재하지 않으면 예외를 던진다. 이렇게 DB에서 가져온 이용자의 정보와 화면에서 입력한 로그인 정보를 비교하게 되고, 일치하면 Authentication 참조를 리턴하고, 일치 하지 않으면 예외를 던진다.

9. 인증이 완료되면 사용자 정보를 가진 Authentication 객체를 SecurityContextHolder에 담은 이후 AuthenticationSuccessHandle를 실행한다.(실패시 AuthenticationFailureHandler를 실행한다.)

# Spring Security를 사용한 인증 인가와 그렇지 않은 인증 인가 구현에 대한 차이

1. 인증 인가를 사용하는 경우, 사용자는 애플리케이션에 로그인해야만 자원에 접근할 수 있습니다. 이를 위해 사용자는 로그인 페이지에 접속하고, 사용자 이름과 비밀번호를 입력해야 합니다. 로그인 정보는 세션(session)에 저장되며, 세션을 통해 인증된 사용자만이 자원에 접근할 수 있습니다.

2. 그러나 그렇지 않은 인증 인가를 사용하는 경우, 사용자는 로그인 없이도 자원에 접근할 수 있습니다. 이 경우 인증 없이 자원에 접근할 수 있는 URL 패턴을 설정해야 합니다. 이를 위해 Spring Security는 antMatchers() 메서드를 사용합니다.

3. 인증 인가를 사용하는 경우, 인증된 사용자만이 자원에 접근할 수 있으므로, 보안성이 높아집니다. 그러나 로그인이 필요하므로 사용자 경험이 저하될 수 있습니다.

4. 반면에 그렇지 않은 인증 인가를 사용하는 경우, 사용자 경험이 좋아질 수 있지만, 보안성이 떨어질 수 있습니다. 인증 없이 자원에 접근할 수 있는 URL 패턴을 설정하게 되면, 인증되지 않은 사용자도 자원에 접근할 수 있게 됩니다.


# Reference
https://velog.io/@kyungwoon/Spring-Security-%EB%8F%99%EC%9E%91-%EC%9B%90%EB%A6%AC
https://m.boostcourse.org/web326/lecture/58997
https://chat.openai.com/chat