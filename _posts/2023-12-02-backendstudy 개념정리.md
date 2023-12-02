---
layout: single
title: "backend memo"
toc: true
toc_sticky: true
toc_label: "목차"
categories: backendstudy
toc_icon: "bars"
tags: [backendstudy]
---

# massage 큐에 대해 설명
서비스들 간에 데이터를 주고 받는 방법중에 하나 
장점 (Decoupling)
service a가 service b,c,d모두에 dependency가 생김
만약 챗서버라 하면 어떤 유저가 메시지를 보냈어 그럼 새로운 메시지가 왔을때 이걸 데이터베이스에 저장도 해야되고 메시지를 받는 유저한테 메시지를 포워드해줘야되고 이메일을 보내줘야될때도 있고 여러가지 디펜던시가 생길수 있다. 그러다 보면 이거의 모든 코드를 한 serviceA에 넣어줘야된다 그럼 점점 복잡해지고 테스트하기어려워지니까 이런 상황에서 메시지 큐를 넣으면 디펜던시가 훨씬 적어진다.
## 레빗엠큐와 카프카 차이점
카프카는 이벤트  브로커이고(업무시간동안 필요한 시간동안 보관가능 데이터 처리후 삭제 하지 않음 (에러해결))
레빗엠큐는 메시지 브로커이다(메시지를 받고 처리하는 브로커 끝나면 삭제)
메시지 브로커는 이벤트 브로커로 역할을 할수 없지만 이벤트 브로커는 메시지 브로커 역할을 할수 있다.


# flask와 django의 차이점

# nosql과 rdbms의 차이

# spring과 spring boot의 차이점

# spring 동작 과정