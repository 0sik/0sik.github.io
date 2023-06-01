---
layout: single
title: "Spring Transaction"
toc: true
toc_sticky: true
toc_label: "목차"
categories: spring
toc_icon: "bars"
tags: [spring]
---

📘 Spring Transaction

# Transaction
- 트랜젝션이란 쪼갤 수 없는 여러 작업들을 논리적으로 묶은 최소 단위로 묶은것이다.

## 특징 

- 원자성(Atomicity)
트랙잭션의 연산은 DB에 모두 반영되던지, 모두 반영되지 않아야 한다. 하나라도 실패한다면 앞서 성공한 것들을원상 복구 시켜야한다.

- 일관성(Consistency)
트랜잭션의 작업 처리 결과는 항상 일관성 있어야 한다.

- 독립성(Isolation)
어떤 트랜잭션도 다른 트랜잭션의 작업에 끼어들 수 없다.

- 지속성(Durability)
트랜잭션이 완료된다면, 결과는 영구적이어야 한다.

