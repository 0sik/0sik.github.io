---
layout: single
title: "TypeScript란?"
toc: true
toc_sticky: true
toc_label: "목차"
categories: typescript
toc_icon: "bars"
tags: [typescript]
---

📘타입 스크립트

# 타입스크립트란?
- 타입스크립트는 자바스크립트에 타입을 부여한 언어이다
- 자바스크립트의 확장된 언어라고 볼 수 있다.

# 장점

## 함수
> TypeScript를 사용하는 가장 큰 이유 중 하나는 정적 타입을 지원한다는 것이다

```
function sum(a,b){
    return a+b;
}
```
위 함수를 정의한 개발자의 의도는 아마도 2개의 숫자 타입 인수를 전달받아 그 합계를 반환하려는 것으로 추측할 수 있다. 하지만 코드상으로는 어떤 타입의 인수를 전달하여야 하는지, 어떤 타입의 반환값을 리턴해야 하는지 명확하지 않다. 따라서 위 함수는 아래와 같이 호출될 수 있다.
```
function sum(a, b) {
  return a + b;
}

sum(10,20) //30
```
이렇게 sum 함수를 이용하여 숫자 10과 20을 더한다. 그러면 원하는 결과인 30을 얻을 수 있다. 그런데 만약 아래와 같이 함수를 호출하면 어떻게 될까?
```
sum('10', '20'); // 1020
```
위 코드는 자바스크립트 문법상 어떠한 문제도 없으므로 자바스크립트 엔진은 아무런 이의 제기없이 위 코드를 실행할 것이다.
이러한 상황이 발생한 이유는 변수나 반환값의 타입을 사전에 지정하지 않는 자바스크립트의 동적 타이핑(Dynamic Typing)에 의한 것이다.

위 함수를 TypeScript의 정적 타이핑(Static Typing)을 사용하여 다시 작성 해보자.
```
function sum(a: number, b: number) {
  return a + b;
}
sum('10', '20');
error TS2345: Argument of type '"10"' is not assignable to parameter of type 'number'.
```
이처럼 TypeScript는 정적 타입을 지원하므로 컴파일 단계에서 오류를 포착할 수 있는 장점이 있다.

명시적인 정적 타입 지정은 개발자의 의도를 명확하게 코드로 기술할 수 있고 이는 코드의 가독성을 높이고 예측할 수 있게 하며 디버깅을 쉽게 할수있다.

## 배열
-javascript(동적언어): 런타임에 타입 결정 /오류 발견
-typescript(정적언어): 컴파일 타임에 타입 결정/ 오류발견
```
function showItems(arr:number[]){ // 배열을 받아서 loop를 돌면서 보여주는 함수
    arr.forEach(item)=>{
        console.log(item);
    });
    }

showItems([1,2,3]); // 문제없이 작동
showItems(1,2,3); // 배열이 아니라 Error
```