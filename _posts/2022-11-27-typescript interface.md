---
layout: single
title: "TypeScript의 interface"
toc: true
toc_sticky: true
toc_label: "목차"
categories: typescript
toc_icon: "bars"
tags: [typescript]
---

📘타입 스크립트

# 객체생성
- 밑에 처럼 user을 object라 정의했을때 user.name을 찍으면 object형식에 name이라는 속성이 없어 에러가 발생한다.
```
let user : object;

user = {
    name : 'xx',
    age : 30
}

console.log(user.name) // object에는 특정 속성값에 대한 정보가 없다
```

# 인터페이스 생성
-User이라는 인터페이스를 만들고 이를 바탕으로 user이라는 객체를 만든다
```
interface User{
    name : string;
    age : number;
}

let user1 : User={
    name  : 'x',
    age : 30
}

user1.age = 10;
user1 .gender = "male"
```
- 여기서 gender이라는 속성이 없어서 에러가 발생한다

```
interface User{
    name : string;
    age : number;
    gender : string;
}

let user1 : User={
    name  : 'x',
    age : 30
}
```

## ?:
- User에는 gender라는 속성을 추가하였지만 그래도 에러가 발생 user1에 속성이 포함되지 않았기 때문
- 성별을 입력을 해도 되고 안해도 되는 속성으로 하려면 User에
> gender? : string;
 
 ## readonly
 - 또한 성별을 객체생성할때만 할당이 가능하고 그 이후에는 설정을 바꾸기 싫다하면 User에
 > readonly gender : string;

## key:value
 - 인터페이스 안에도 key :value를 입력받을수 있게 할 수 있다 User에
 > ```[grade: number] : string;```
```
let user1 : User={
    name  : 'x',
    age : 30
    1 : 'A',
    2 : 'B 
}
 ```
## type 정의
 - type을 정의하여 string이나 number을 대체할수있다
 > type Score = 'A'|'B';
 > ``` [grade:number] : Score; ```
 ```
 let user1 : User={
    name  : 'x',
    age : 30,
    birthYear : 2000 ,
    1 : 'A',
    2 : 'B'
}
 ```


 ## 인터페이스로 함수 정의  
 - 인터페이스로 함수를 정의할수 있다.
 ```
interface ADD {
    (num1:number,num2:number): number;
}

const add:ADD = function(x,y){
    return x+y;
}

add(10,20);

// 성인인지 비교하는 함수
interface IsAdult{
    (age:number) : boolean;
}

const a3 : IsAdult = (age) =>{
    return age>19;
}

a3(33) //true
```

# 인터페이스로 클래스 정의
 
## 구현
```
interface Car{
    color : string;
    wheels : number;
    start(): void;
}

class Bmw implements Car{
    color: string;
    wheels = 4;
   constructor(c:string){
    this.color=c;
   } 
   start(): void {
       console.log('go');
   }
}
const b3 = new Bmw('green');
console.log(b3)
b3.start(); // go
```
## 확장
```
//extends
interface Benz extends Car{
    door : number;
    stop(): void;
}

const benz : Benz={
    door : 5,
    stop(){
        console.log('stop');
    },
    color : 'black',
    wheels : 4,
    start(): void {
        console.log('go');
    }
}
```