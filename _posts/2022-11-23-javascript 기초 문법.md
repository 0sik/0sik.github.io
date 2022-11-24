---
layout: single
title: "자바 스크립트 기초 문법"
toc: true
toc_sticky: true
toc_label: "목차"
categories: javascript
toc_icon: "bars"
tags: [javascript]
---

📘자바 스크립트

# 변수 선언
1. let 
- 변할 수 있는 값
- let grade = "F";
- grade = "A+"; 

2. const 
- 절대로 바뀌지 않는 상수 (가급적 대문자로 입력)
- 수정 X

변수 설정에 console 찍을때
```
const name = "mike";
const message = `My name is ${name}`;

console.log(message);

```
사용

# 대화 상자
- 단점 : 스크립트 일시 정지, 스타일링X
1. alert 
- 알려줌
- 메시지를 띄우기 사용자에게 메시지 알리기
- 확인 버튼만 있음
2. prompt
- 입력받음
- 사용자에게 값을 입력받을때 사용
- const name = prompt("예약일을 입력해주세요","2020-10-");
- 여기서 앞 인수는 메시지가 되고 , 뒤에 인수는 입력받을 디폴트 값이 된다
3. confirm
- 확인 받음
- 확인과 취소 버튼이 있음
- 확인을 누르면 변수에 ture 취소를 누르면 false

# 형변환
1. String()
2. Number()
3. Boolean()
  - 0 , "" , null, nudefined , NaN 뻬고는 다 true

# 논리 연산자
- || (or)
- && (and)
- ! (not)

# 함수
- 보통 함수 선언문으로 씀
- 
1. 함수 선언문 : 어디서든 호출 가능
```
sayHello();
function sayHello(){
  consloe.log('hello');
}
```
  - 자바 스크립트는 실행전 초기화 단계에서 모든 함수가 실행된다
2. 함수 표현식 : 코드에 도달하면생성
```
let sayHello = function(){
  consloe.log('hello');
}
sayHello();
```
  - 자바 스크립트가 한줄씩 읽으면서 실행하고 해당 함수에 도달했을때 함수가 생성되고 사용가능하다

3. 화살표 함수
```
const add = (num1,num2)=>(
  num1+num2 //한줄일 경우에 이렇게 쓸수있음
);
```

# 객체
