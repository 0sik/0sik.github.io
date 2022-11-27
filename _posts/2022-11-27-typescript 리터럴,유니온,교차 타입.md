---
layout: single
title: "리터럴,유니온,교차타입"
toc: true
toc_sticky: true
toc_label: "목차"
categories: typescript
toc_icon: "bars"
tags: [typescript]
---

📘타입 스크립트

# Literal Type(리터럴)

- 리터럴 타입이란 변하지 않는 값이다 
- ex: const userName = "bob"

## 타입을 명시하고 쓰기

-인터 페이스 안에 타입을 명시하고 쓸수가 있다


```
type job = "police"|"developer"|"teacher";

interface User {
    name : string,
    job : "developer"
}
```

# union type(유니온)
- 유니온 타입이란 변수가 여러가지 타입을 갖는것을 의미한다.
- ex : name: number|string

## 인터페이스 유니온
- 인터페이스로 유니온함수를 만드려면 다음과 같다

```
interface Car{
    name:"car";
    color : string;
    start():void;
}

interface Mobile{
    name:'mobile';
    color:string;
    call():void;
}

function getGift(gift:Car|Mobile){
    console.log(gift.color);
    if(gift.name === "car"){
    gift.start();
    }
    else{
        gift.call();
    }

}
```

- 위 처럼 gift가 car이 될수있고 mobile이 될수있다
- car,mobile두개의 조건을 다 정의 해줘야 한다.

# Intersection Type (교차 타입)
- 여러개의 인터페이스를 가지는 변수를 선언할때 교차타입이라고한다.

```
interface Car1{
    name:string;
    start():void;
}
interface Toy{
    name:String;
    color:String;
    price:Number;
}
const toyCar:Toy|Car1={
    name:"타요",
    start(){},
    color:"blue",
    price:1000,
};
```

- 위 코드 toy와 car의 교차타입으로 쓰려면 두개의 인터페이스의 속성을 다 가지고 있어야 한다