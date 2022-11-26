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

# 객체

## 객체 생성
```
const superman = }
  name : 'clark',
  age : 33,
  }
```

## 객체 접근
superman.name //'clark'
superman['age'] // 33

## 객체 추가
superman.gender = 'male';
superman['hairColor'] = 'black';

## 객체 삭제
delete superman.hairColor;

## 객체 확인
```

function isAdult(user){
    if(!('age' in user) || // user에 age가 없거나
     user.age <20){ // 20살 미만이거나
        return false;
    } 
    return true;
}

const Mike1 = {
    name : 'Mike',
    age : 30
};

const Jane = {
    name : 'jane'
};

console.log(isAdult(Mike1)) // true
console.log(isAdult(Jane)) // false

```

## 단축 프로퍼티
```
function makeObject(name,age){
    return{
        name,//name : name,
        age,//age : age,
        hobby : 'football'
    }
}

const Mike = makeObject("Mike",30); // 객체 생성됨
```

## 객체 순회 for .. in
```
//객체 for .. in
const Mike3 = {
    name : "Mike",
    age :30
}

for (x in Mike){
    console.log(Mike[x]) // Mike가 가지고 있는 key 값 출력
}
```

## 객체 Method 

```
const super man={
    name :'clark',
    age:33,
    fly(){  //fly : function() 을 줄여 쓴것임
        console.log("날아갑니다")
    }
}

```

## 객체 this 
 
- 일반 함수 에서의 this
```
const user = {
    name = 'mike',
    sayHello(){
        console.log{'Hello i'm ${this.name}}
    }
}

```
- 화살표 함수 에서의 this
```
let boy ={
    name : 'mike',
    sayHello :() =>{
        console.log(this); // 전역 객체 *브라우저 환경 : window *node js : global
    }
}

boy.sayHello(); // this!=boy
```
> 화살표 함수는 일반 함수와는 달리 자신만의 this를 가지지 않음 화살표 함수 내부에서 this를 사용하면, 그 this 는 외부에서 값을 가져옴