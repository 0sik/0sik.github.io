---
layout: single
title: "TypeScript의 함수"
toc: true
toc_sticky: true
toc_label: "목차"
categories: typescript
toc_icon: "bars"
tags: [typescript]
---

📘타입 스크립트

# 함수

-각 매개변수의 타입을 입력해주고 괄호 뒤에는 이 함수가 반환하는 타입을 입력해준다

```
function add (num1:number,num2:number):number{ 
    return num1+num2;
}
```

- 아무것도 반환하지 않으면 :number -> :void로 바꿔준다

```
//기본 함수
function hello(name?:string){
    return `hello,${name||"world"}`;
}
const result= hello();
const result2 = hello("sam");

console.log(result);
console.log(result2);
```

## 매개변수 앞 undefined
- 매개변수 앞에는 ? 를 쓰지 못한다 다음 상황은 에러가 발생한다

```
function hello3(age?:number,name:string):string{
    if(age!==undefined){
        return`hello${name}.you are ${age}`;
    }
    else{
        return `hello${name}`;
    }
}
console.log(hello3("sam")); // 에러발생
console.log(hello3(30,"sam"));
```

- 이같은 상황을 해결하기 위해서는 다음과 같이 코드를 작성해야 한다

```
function hello3(age:number|undefined,name:string):string{
    if(age!==undefined){
        return`hello${name}.you are ${age}`;
    }
    else{
        return `hello${name}`;
    }
}

console.log(hello3(30,"sam"));
console.log(hello3(undefined,"sam"));
```

## 나머지 매개변수
- 나머지 매개변수는 개수가 매번 바뀔수 있을때 사용한다 

```
function add3(...nums:number[]){
    return nums.reduce((result,num)=>result+num,0);
}

add3(1,2,3);//6
add3(1,2,3,4,5,6,7,8,9,10)//55
```

## this
- this 가 어디 객체인지 표시하기 위해서는 매개변수에 선언 해줘야한다.

```
interface User3 {
    name : string;
}
const Sami :User3={name:'sami'}

function showName(this:User3){
    console.log(this.name)
}

const sami1 = showName.bind(Sami);
sami1();
```

# 오버로드
- 밑에 코드처럼 age 가 숫자가 될수 있고 문자가 될수있을때 숫자면 user을 반환 문자면 string을 반환하는 코드이다

- 함수만 정의했을때는 별 문제 없어 보이지만 변수설정을하면 에러가 발생한다

```
interface User{
    name:string;
    age:number;
}
function join(name:string,age:number|string):User|string{
    if(typeof age ==="number"){
        return{
            name,
            age,
        };
    }else{
        return " 나이는 숫자로 입력해주세요"
    }
}
const sam:User = join("sam",30); // 에러
const jane : string = join("jain","30");  //에러
```

-이러한 문제를 해결하기 위해서 오버로드를 쓴다



>``` function join(name:string,age:number):User;```

>``` function join(name:string,age:string):string;```