---
layout: single
title: "TypeScript์ interface"
toc: true
toc_sticky: true
toc_label: "๋ชฉ์ฐจ"
categories: typescript
toc_icon: "bars"
tags: [typescript]
---

๐ํ์ ์คํฌ๋ฆฝํธ

# ๊ฐ์ฒด์์ฑ
- ๋ฐ์ ์ฒ๋ผ user์ object๋ผ ์ ์ํ์๋ user.name์ ์ฐ์ผ๋ฉด objectํ์์ name์ด๋ผ๋ ์์ฑ์ด ์์ด ์๋ฌ๊ฐ ๋ฐ์ํ๋ค.

```
let user : object;

user = {
    name : 'xx',
    age : 30
}

console.log(user.name) // object์๋ ํน์  ์์ฑ๊ฐ์ ๋ํ ์ ๋ณด๊ฐ ์๋ค
```

# ์ธํฐํ์ด์ค ์์ฑ
-User์ด๋ผ๋ ์ธํฐํ์ด์ค๋ฅผ ๋ง๋ค๊ณ  ์ด๋ฅผ ๋ฐํ์ผ๋ก user์ด๋ผ๋ ๊ฐ์ฒด๋ฅผ ๋ง๋ ๋ค

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

- ์ฌ๊ธฐ์ gender์ด๋ผ๋ ์์ฑ์ด ์์ด์ ์๋ฌ๊ฐ ๋ฐ์ํ๋ค

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
- User์๋ gender๋ผ๋ ์์ฑ์ ์ถ๊ฐํ์์ง๋ง ๊ทธ๋๋ ์๋ฌ๊ฐ ๋ฐ์ user1์ ์์ฑ์ด ํฌํจ๋์ง ์์๊ธฐ ๋๋ฌธ
- ์ฑ๋ณ์ ์๋ ฅ์ ํด๋ ๋๊ณ  ์ํด๋ ๋๋ ์์ฑ์ผ๋ก ํ๋ ค๋ฉด User์

> gender? : string;
 
 ## readonly
 - ๋ํ ์ฑ๋ณ์ ๊ฐ์ฒด์์ฑํ ๋๋ง ํ ๋น์ด ๊ฐ๋ฅํ๊ณ  ๊ทธ ์ดํ์๋ ์ค์ ์ ๋ฐ๊พธ๊ธฐ ์ซ๋คํ๋ฉด User์

 > readonly gender : string;

## key:value
 - ์ธํฐํ์ด์ค ์์๋ key :value๋ฅผ ์๋ ฅ๋ฐ์์ ์๊ฒ ํ  ์ ์๋ค User์

 > ```[grade: number] : string;```

```
let user1 : User={
    name  : 'x',
    age : 30
    1 : 'A',
    2 : 'B 
}
 ```

## type ์ ์
 - type์ ์ ์ํ์ฌ string์ด๋ number์ ๋์ฒดํ ์์๋ค

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


 ## ์ธํฐํ์ด์ค๋ก ํจ์ ์ ์  
 - ์ธํฐํ์ด์ค๋ก ํจ์๋ฅผ ์ ์ํ ์ ์๋ค.

 ```
interface ADD {
    (num1:number,num2:number): number;
}

const add:ADD = function(x,y){
    return x+y;
}

add(10,20);

// ์ฑ์ธ์ธ์ง ๋น๊ตํ๋ ํจ์
interface IsAdult{
    (age:number) : boolean;
}

const a3 : IsAdult = (age) =>{
    return age>19;
}

a3(33) //true
```

# ์ธํฐํ์ด์ค๋ก ํด๋์ค ์ ์
 
## ๊ตฌํ

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

## ํ์ฅ

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