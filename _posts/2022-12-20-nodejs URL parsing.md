---
layout: single
title: "URL parsing"
toc: true
toc_sticky: true
toc_label: "목차"
categories: nodejs
toc_icon: "bars"
tags: [nodejs]
---

📘nodejs

# URL parsing
먼저 화면 이동은 기본적으로 a태그 씀
``` <a href=/?id=1></a> ```
먼저 url 모듈을 import 해줘야한다
> var url = require('url');

그 다음 서버 생성 
> var app = http.createServer(function(request,response)

그 다음 url을 request 받고
> var _url = request.url;

만약 url 이 locallhost:3000/?id=HTML이라면 id 값을 저장할 변수 지정
> var queryData = url.parse(_url,true).query;
> console.log(queryData.id) // HTML

url별로 화면 구성하는법
> var pathname = url.parse(_url, true).pathname;
```
if(pathname === '/'){
      if(queryData.id === undefined){
        });
      } else {

    } else if(pathname === '/create'){
        `);
        response.writeHead(200);
        response.end(template);
      });
    } else {
      response.writeHead(404);
      response.end('Not found');
    }

```

# file 
1. 파일 읽기
data 디렉토리 안에 파일 HTML이 존재할경우 queryData.id를 통해 불러옴
> ```fs.readFile(`data/${queryData.id}`, 'utf8',function(err,data)){
> var template = `${data}```

2. 파일 목록 알아내기
> ```var testFolder = './data'```
> ```fs.readdir(testFolder,function(error,filelist)```

# 동기적, 비동기적
동기적 : 어떤 작업을 요청했을 때 그 작업이 종료될때 까지 기다린 후 다음 작업을 수행
비동기적 : 어떤 작업을 요청했을 때 그 작업이 종료될때 까지 기다리지 않고 다른 작업을 하고 있다가, 요청했던 작업이 종료되면 그에 대한 추가 작업을 수행하는 방식
> var result = fs.readFileSync('syntax/sample.txt','utf8'); // 동기적
> fs.readFile('syntax/sample.txt','tuf8',function(err,result)) // 비동기적
> node.js의 성능을 최대로 끌어오리기 위해서는    비동기적 선호
