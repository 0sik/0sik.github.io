---
layout: single
title: "Rest Api란, api이용해 자기자신에게 카톡보내기"
toc: true
toc_sticky: true
toc_label: "목차"
categories: python
toc_icon: "bars"
tags: [python]
---

📘파이썬

# Api란
- Application Programming Interface
- 소프트웨어가 다른 소프트웨어로부터 지정된 형식으로 요청, 명령을 받을 수 있는 수단을 api라한다
  
# Rest Api란
- 정보들이 주고받아지는데 있어서 개발자들 사이에 널리 쓰이는 일종의 형식이다
- 유체국의 송장처럼 이용자들이 채워넣는 형식이 있듯, 기술이나 제품이 아니라 형식이다
- 어떤 언어든, 프레임워크든 이 형식에 맞춰서 기능을 만들어 내면 된다 
- 서버에 REST API로 요청을 보낼 때는 HTTP란 규약에 따라 신호를 전송한다
- GET : 데이터를 Read, 조회하는데 사용함
- Post : Create, 새로운 정보를 추가하는데 사용 (body에 실어 보낸다)
- Put, Patch : 변경 , update될 새정보들을 body에 실어 보낸다 
- Delete : 삭제할때
> HTTP요청을 보낼때 어떤 URI에 어떤 메소드를 사용할지(+기타) 개발자들 사이에 널리 지켜지는 약속
> 형식이기 때문에 , 기술에 구애 받지 않는다.

# api이용해 자기자신에게 카톡보내기

1.내 애플리 케이션에 가서 애플리케이션 추가

2.플랫폼에 들어가서 Web에 사이트 도메인 https://google.co.kr 등록(크롬기준)

3.카카오 로그인에 활성화 설정 on 으로 바꾸기

4.Redirect URL 에 https://example.com/oauth 로 설정

5.동의 항목 바꾸기 상태를 동의로 바꿔줘야함 거의 다
# 주피터로 연결
```
https://kauth.kakao.com/oauth/authorize?client_id=s
{RESTAPI키}&redirect_uri={RedirectURL}&response_type=code&scope=talk_message
```

을 치고Accept하면
>https://example.com/oauth/?code={코드} 라고 뜸

```
# 라이브러리 호출
import requests
import json
#카카오톡 메시지 API
url = "https://kauth.kakao.com/oauth/token"
data = {
    "grant_type" : "authorization_code",
    "client_id" : "{REST API}",
    "redirect_url" : "https://localhost:3000",
    "code" : "{코드}"
}
response = requests.post(url, data=data)
tokens = response.json()
print(tokens)
#kakao_code.json 파일 저장
with open("kakao_code.json", "w") as fp:
    json.dump(tokens, fp)
```

토큰을 생성도해보고 프린트해봤고
json파일에 저장까지해봤다

```
url = "https://kapi.kakao.com/v2/api/talk/memo/default/send"
headers = {
    "Authorization": "Bearer " + "{access_token}"
}
data = {
    "template_object" : json.dumps({ "object_type" : "text",
                                     "text" : "Google 뉴스: drone",
                                     "link" : {
                                                 "web_url" : "https://www.google.co.kr/search?q=drone&source=lnms&tbm=nws",
                                                 "mobile_web_url" : "https://www.google.co.kr/search?q=drone&source=lnms&tbm=nws"
                                              }
    })
}
response = requests.post(url, headers=headers, data=data)
if response.json().get('result_code') == 0:
    print('메시지를 성공적으로 보냈습니다.')
else:
    print('메시지를 성공적으로 보내지 못했습니다. 오류메시지 : ' + str(response.json()))
 ``` 

메시지 전송 완료