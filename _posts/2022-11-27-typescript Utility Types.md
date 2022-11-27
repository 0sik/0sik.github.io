---
layout: single
title: "유틸리티 타입"
toc: true
toc_sticky: true
toc_label: "목차"
categories: typescript
toc_icon: "bars"
tags: [typescript]
---

📘타입 스크립트

# keyof
- 키 값들을 유니온 형태로 받을수 있다

```
interface bot{
    id:number;
    name:string;
    age:number;
    gender:"m"|"f";
}
```

- 다음과 같은 interface가 있을때

```
type botKey = keyof bot;  
```

- 이렇게 keyof 를 쓰게 되면 

```
'id' | ' name'| 'age' | 'gender'
```

- 중 하나를 받을수 있는 변수가 된다

```
const bk:botKey = "name";  
```

- 인터페이스의 키 값중 하나를 입력받을수 있다.

# Partial<T>
- 프로포티를 모두 옵셔널로 바꿔준다
- 일부만 사용하는게 가능해준다
- id : number; ==> id?: number로 바꿔준다

```
let admin : Partial<bot>={
    id:1,
    name:'b'
}
```

# Required<T>
- 모든 프로포티를 필수로 바꿔준다
- 인터페이스에 id ?: number; ==> id: number로 바꿔준다

 # readonly
 - 또한  객체생성할때만 할당이 가능하고 그 이후에는 설정을 바꾸기 싫다하면 bot에

 > readonly name : string;

 # Record<K,T>
 - K는 키값이고 T는 타입이다

 ```
type Grade = "1"|"2"|"3"|"4";
type Score1 = "A"|"B"|"C"|"D";
const score:Record<Grade,Score1> = {
    1: "A",
    2 :"B",
    3 :"C",
    4 :"D"
}
 ```

```
interface bot{
    id:number;
    name:string;
    age:number;
}

function isValid(user:bot){
    const about : Record<keyof bot, boolean>={
        id : user.id >0,
        name:user.name !=="",
        age:user.age>0,
    }
}
```

# Pick<T,K>
- 인터페이스에서 K프로퍼티만 사용하고싶을때 사용
- 위에 bot인터페이스가 있을때 id랑 name 만 쓰고싶을때 사용

```
cost admin : Pick<bot,"id"|"name">={
    id:0,
    name:"bob"
};
```

# Omit<T,K>
- 인터페이스에서 K프로퍼티를 빼고싶을때 사용
- 위에 bot 인터페이스가 있을때 age를 빼고싶을때 사용

```
cost admin : Omit<bot,"age">={
    id:0,
    name:"bob"
};

```

# Exclude<T1,T2>
- type1에서 type2를 제외하고 사용하는 방법

```
type t1 = stirng|number|boolean;
type t2 = Exclude<t1,number|string>;  ==> boolean타입만 남게 됨
```

# NonNullabe<Type>
- Null을 제외한 타입을 생성 undifined도 제외

```
type t1 = stirng|number|boolean|null|undefined;
type t2 = NonNullabe<t1>;  ==> stirng number boolean 타입만 남게됨
```