---
layout: single
title: "정규화"
toc: true
toc_sticky: true
toc_label: "목차"
categories: database
toc_icon: "bars"
tags: [database]
---
📘 정규화

# 정규화

정규화는 이상현상이 있는 릴레이션을 분해하여 이상현상을 없애는 과정이다. 이상현상이 존재하는 릴레이션을 분해하여 여러개의 릴레이션을 생성하게 된다. 이를 단계별로 구분하여 정규형이 높아질수록 이상현상은 줄어들게 된다

# 정규화의 장점 
1. 데이터베이스 변경 시 이상 현상(Anomaly)을 제거할 수 있다.
2. 정규화된 데이터베이스 구조에서는 새로운 데이터 형의 추가로 인한 확장 시, 그 구조를 변경하지 않아도 되거나 일부만 변경해도 된다.
3. 데이터베이스와 연동된 응용 프로그램에 최소한의 영향만을 미치게 되어 응용프로그램의 생명을 연장시킨다.

# 정규화의 단점
1. 릴레이션의 분해로 인해 릴레이션 간의 JOIN연산이 많아진다.
2. 질의에 대한 응답 시간이 느려질 수도 있다. 데이터의 중복 속성을 제거하고 결정자에 의해 동일한 의미의 일반 속성이 하나의 테이블로 집약되므로 한 테이블의 데이터 용량이 최소화되는 효과가 있다. 
따라서 데이터를 처리할 때 속도가 빨라질 수도 있고 느려질 수도 있다.
3. 만약 조인이 많이 발생하여 성능 저하가 나타나면 반정규화(De-normalization)를 적용할 수도 있다.


# 정규화의 목표
1. 테이블 간에 중복된 데이터를 호용하지 않는다
2. 중복된 데이터를 허용하지 않음으로써 무결성을 유지할수있으며, DB의 저장 용량 역시 줄일수있다.

## 제 1 정규화
제 1 정규화란 테이블의 컬럼이 인자값을 갖도록 테이블을 분해하는것이다. 원자값이란 하나의 값이란 뜻이다.

## 제 2 정규화
제 2 정규화란 제 1 정규화를 진행한 테이블에 대해 완전 함수 종속을 만족하도록 테이블을 분해하는것이다. 여기서 완전 함수 종속이라는 것은 기본키의 부분집합이 결정자가 되어선 안된다는것을 의미한다.

## 제 3 정규화
제3정규화란 제2정규화를 진행한 테이블에 대해 이행적 종속을 없애도록 테이블을 분해하는것이다 

## BCNF정규화
BCNF정규화란 제 3정규화를 진행한 테이블에 대해 모든 결정자가 후보키가 되도록 테이블을 분해하는 것이다.

## 그 이후 
보통 정규화는 BCNF 까지만 하는 경우가 많다. 그 이상 정규화를 하면 정규화의 단점이 나타날 수도 있다.
4정규형 이상은 다음 게시물을 참고하자


참고 : https://mangkyu.tistory.com/110
참고 : https://code-lab1.tistory.com/48 [코드 연구소:티스토리]