---
layout: single
title: "OAuth 2.0 동작 방식의 이해"
toc: true
toc_sticky: true
toc_label: "목차"
categories: backendstudy
toc_icon: "bars"
tags: [backendstudy]
---

📘OAuth 2.0 동작 방식의 이해 ( && JWT 토큰과 토큰 관리 방식 )

# OAuth 2.0

- 인증을 위한 개방형 표준 프로토콜이다.
- Third-Party프로그램에게 리소스 소유자를 대신하여 리소스 서버에서 제공하는 자원에 대한 접근 권한을 위임하는 방식을 제공한다.
- 구글,페이스북,카카오,네이버 등 외부 소셜 계정을 기반으로 간편하게 인증하는 기능

## OAuth 2.0의 4가지 역할
1. Resource Owner 
    - 리소스 소유자입니다. 본인의 정보에 접근할 수 있는 자격을 승인하는주체
    - 예로 구글 로그인을 할 사용자
    - 클라이언트를 인증하는 역할을 수행하고, 인증이 완료되면 동의를 통해 권한 획득자격을 클라이언트에게 부여

2. Client
    - Resource Owner의 리소스를 사용하고자 접근 요청을 하는 어플리케이션

3. Resource Server 
    - Resource Owner의 정보가 저장되어 있는 서버

4. Authorization Server
    - 권한 서버
    - 인증/인가를 수행하는 서버로 클라이언트의 접근 자격을 확인하고 Access Token을 발급하여 권한을 부여하는 역할을 수행

## OAuth 2.0의 주요 용어
- Authentication(인증) : 인증,접근 자격이 있는지 검증하는 단계
- Authorization(인가) : 자원에 접근할 권한을 부여하고 리소스 접근  권한이 담긴 AccessToken을 제공한다
- Access Token : 리소스 서버에게서 리소스 소유자의 정보를 획득할 때 사용되는 만료 기간이 있는 Token
- Refresh Token : Access Token만료시 이를 재발급 받기 위한 용도로 사용하는 Token

## OAuth 2.0 권한 부여 방식

- https://velog.io/@kimjaejung96/OAuth2.0-%EA%B0%9C%EB%85%90-%EB%B0%8F-%EC%9E%91%EB%8F%99%EB%B0%A9%EC%8B%9D

### Authorization Code Grant │ 권한 부여 승인 코드 방식
권한 부여 승인을 위해 자체 생성한 Authorization Code를 전달하는 방식으로 많이 쓰이고 기본이 되는 방식입니다. 간편 로그인 기능에서 사용되는 방식으로 클라이언트가 사용자를 대신하여 특정 자원에 접근을 요청할 때 사용되는 방식입니다. 보통 타사의 클라이언트에게 보호된 자원을 제공하기 위한 인증에 사용됩니다. Refresh Token의 사용이 가능한 방식입니다.

권한 부여 승인 요청 시 response_type을 code로 지정하여 요청합니다. 이후 클라이언트는 권한 서버에서 제공하는 로그인 페이지를 브라우저를 띄워 출력합니다. 이 페이지를 통해 사용자가 로그인을 하면 권한 서버는 권한 부여 승인 코드 요청 시 전달받은 redirect_url로 Authorization Code를 전달합니다. Authorization Code는 권한 서버에서 제공하는 API를 통해 Access Token으로 교환됩니다.

 

### Implicit Grant │ 암묵적 승인 방식
자격증명을 안전하게 저장하기 힘든 클라이언트(ex: JavaScript등의 스크립트 언어를 사용한 브라우저)에게 최적화된 방식입니다.

암시적 승인 방식에서는 권한 부여 승인 코드 없이 바로 Access Token이 발급 됩니다. Access Token이 바로 전달되므로 누출의 위험을 방지하기 위해 만료기간을 짧게 설정하여 전달됩니다.

Refresh Token 사용이 불가능한 방식이며, 이 방식에서 권한 서버는 client_secret를 사용해 클라이언트를 인증하지 않습니다. Access Token을 획득하기 위한 절차가 간소화되기에 응답성과 효율성은 높아지지만 Access Token이 URL로 전달된다는 단점이 있습니다.

권한 부여 승인 요청 시 response_type을 token으로 설정하여 요청합니다. 이후 클라이언트는 권한 서버에서 제공하는 로그인 페이지를 브라우저를 띄워 출력하게 되며 로그인이 완료되면 권한 서버는 Authorization Code가 아닌 Access Token를 redirect_url로 바로 전달합니다.

### Resource Owner Password Credentials Grant │ 자원 소유자 자격증명 승인 방식
간단하게 username, password로 Access Token을 받는 방식입니다.

클라이언트가 타사의 외부 프로그램일 경우에는 이 방식을 적용하면 안됩니다. 자신의 서비스에서 제공하는 어플리케이션일 경우에만 사용되는 인증 방식입니다. Refresh Token의 사용도 가능합니다.

Authorization Grant: Password

위와 같이 흐름은 간단합니다. 제공하는 API를 통해 username, password을 전달하여 Access Token을 받는 것입니다. 중요한 점은 이 방식은 권한 서버, 리소스 서버, 클라이언트가 모두 같은 시스템에 속해 있을 때 사용되어야 하는 방식이라는 점입니다.

 

### Client Credentials Grant │ 클라이언트 자격증명 승인 방식
클라이언트의 자격증명만으로 Access Token을 획득하는 방식입니다.

OAuth2의 권한 부여 방식 중 가장 간단한 방식으로 클라이언트 자신이 관리하는 리소스 혹은 권한 서버에 해당 클라이언트를 위한 제한된 리소스 접근 권한이 설정되어 있는 경우 사용됩니다. 이 방식은 자격증명을 안전하게 보관할 수 있는 클라이언트에서만 사용되어야 하며, Refresh Token은 사용할 수 없습니다.

# JWT란
- 웹에서 사용되는 JSON 형식의 토큰에 대한 표준 규격인데요. 주로 사용자의 인증(authentication) 또는 인가(authorization) 정보를 서버와 클라이언트 간에 안전하게 주고 받기 위해서 사용
- Authorization HTTP 헤더를 Bearer <토큰>으로 설정하여 클라이언트에서 서버로 전송되며, 서버에서는 토큰에 포함되어 있는 서명(signature) 정보를 통해서 위변조 여부를 빠르게 검증할 수 있게 함

- API 서버는 로그인 요청이 완료되면 클라이언트에게 회원을 구분할 수 있는 정보를 담은 JWT를 생성하여 전달합니다. 그러면 클라이언트는 이 JWT를 헤더에 담아서 요청을 하게 됩니다. 권한이 필요한 요청이 있을 때 마다 API 서버는 헤더에 담긴 JWT 값을 확인하고 권한이 있는 사용자인지 확인하고 리소스를 제공하게 됩니다.

- JSON 객체를 암호화 하여 만든 문자열 값으로 위, 변조가 어려운 정보라고 할 수 있습니다. 또, 다른 토큰들과 달리 토큰 자체에 데이터를 가지고 있다는 특징이 있습니다. JWT의 이러한 특징 때문에 사용자의 인증 요청시 필요한 정보를 전달하는 객체로 사용할 수 있습니다.



# JWT와 OAuth 차이점
WT가 과일이라면 OAuth는 과일을 담는 상자라고 볼 수 있다. 
JWT는 Token의 한 형식이고, OAuth는 하나의 Framework이다.

- OAuth가 Framework인 이유

    1. 토큰을 요청할 때 사용할 수 있어야하는 요청 및 응답의 순서와 형식만 있다.

    2. 각기 다른 시나리오에서 어떤 방식으로 권한 부여 유형을 사용할지 정한다.

그리고 JWT는 이러한 Framework에서 발생하는 산출물로 볼 수 있다.

물론 Auth Framework를 통해 나온 OAuth Bearer token과 단순한 JWT 토큰은 차이가 있다.

OAuth Token은 어떤 사용자의 정보와 같은 중요한 정보가 있는 토큰이 아니다. 그래서 이 토큰을 사용하는 사용자는 이 토큰이 가지고 있는 정보에 대해서 아는 바가 전혀 없다. 

OAuth Token이 가지고 있는 정보는 일련의 랜덤한 문자열인데, 이는 일종의 Pointer로 OAuth Framework로 들어가서 해당 정보가 저장되어 있는 주소를 확인할 수 있는 인식표이다.
물론 이때 토큰이 JWT 유형의 토큰이 될 수도 있다.
반대로 JWT 토큰은 명확한 정보를 가지고 있는 토큰이다. 

토큰의 크기는 300 ~ 500 byte. 혹은 가지고 있는 속성 정보에 따라 더 커지기도 한다.

이때문에 데이터베이스에서 사용자 정보를 조작하더라도 토큰에 직접 적용할 수 없는 문제점이 있고, 토큰이 커지면서 주고 받는 데이터 트래픽 크기에 영향을 미칠 수 있는 단점이 있다.



# Reference
https://blog.naver.com/mds_datasecurity/222182943542
https://charming-kyu.tistory.com/36
https://velog.io/@kimjaejung96/OAuth2.0-%EA%B0%9C%EB%85%90-%EB%B0%8F-%EC%9E%91%EB%8F%99%EB%B0%A9%EC%8B%9D
https://www.daleseo.com/jwt/
https://lewis-kku.tistory.com/34
https://lewis-kku.tistory.com/19