---
layout: single
title: "URL parsing"
toc: true
toc_sticky: true
toc_label: "๋ชฉ์ฐจ"
categories: nodejs
toc_icon: "bars"
tags: [nodejs]
---

๐nodejs

# URL parsing
๋จผ์  ํ๋ฉด ์ด๋์ ๊ธฐ๋ณธ์ ์ผ๋ก aํ๊ทธ ์
``` <a href=/?id=1></a> ```
๋จผ์  url ๋ชจ๋์ import ํด์ค์ผํ๋ค
> var url = require('url');

๊ทธ ๋ค์ ์๋ฒ ์์ฑ 
> var app = http.createServer(function(request,response)

๊ทธ ๋ค์ url์ request ๋ฐ๊ณ 
> var _url = request.url;

๋ง์ฝ url ์ด locallhost:3000/?id=HTML์ด๋ผ๋ฉด id ๊ฐ์ ์ ์ฅํ  ๋ณ์ ์ง์ 
> var queryData = url.parse(_url,true).query;
> console.log(queryData.id) // HTML

url๋ณ๋ก ํ๋ฉด ๊ตฌ์ฑํ๋๋ฒ
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
1. ํ์ผ ์ฝ๊ธฐ
data ๋๋ ํ ๋ฆฌ ์์ ํ์ผ HTML์ด ์กด์ฌํ ๊ฒฝ์ฐ queryData.id๋ฅผ ํตํด ๋ถ๋ฌ์ด
> ```fs.readFile(`data/${queryData.id}`, 'utf8',function(err,data)){
> var template = `${data}```

2. ํ์ผ ๋ชฉ๋ก ์์๋ด๊ธฐ
> ```var testFolder = './data'```
> ```fs.readdir(testFolder,function(error,filelist)```

# ๋๊ธฐ์ , ๋น๋๊ธฐ์ 
๋๊ธฐ์  : ์ด๋ค ์์์ ์์ฒญํ์ ๋ ๊ทธ ์์์ด ์ข๋ฃ๋ ๋ ๊น์ง ๊ธฐ๋ค๋ฆฐ ํ ๋ค์ ์์์ ์ํ
๋น๋๊ธฐ์  : ์ด๋ค ์์์ ์์ฒญํ์ ๋ ๊ทธ ์์์ด ์ข๋ฃ๋ ๋ ๊น์ง ๊ธฐ๋ค๋ฆฌ์ง ์๊ณ  ๋ค๋ฅธ ์์์ ํ๊ณ  ์๋ค๊ฐ, ์์ฒญํ๋ ์์์ด ์ข๋ฃ๋๋ฉด ๊ทธ์ ๋ํ ์ถ๊ฐ ์์์ ์ํํ๋ ๋ฐฉ์
> var result = fs.readFileSync('syntax/sample.txt','utf8'); // ๋๊ธฐ์ 
> fs.readFile('syntax/sample.txt','tuf8',function(err,result)) // ๋น๋๊ธฐ์ 
> node.js์ ์ฑ๋ฅ์ ์ต๋๋ก ๋์ด์ค๋ฆฌ๊ธฐ ์ํด์๋    ๋น๋๊ธฐ์  ์ ํธ
