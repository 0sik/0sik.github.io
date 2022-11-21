---
layout: single
title: "병원 api 이용하여 데이터 받기"
toc: true
toc_sticky: true
toc_label: "목차"
categories: phthon
toc_icon: "bars"
tags: [phthon]
---

📘파이썬

# 병원 위치 api 받기

병원 위치 api를 이용하려면 공공데이터 에서 주어진 url 형식에 맞춰서 url을 설정해 줘야 한다

>https://openapi.gg.go.kr/GgHosptlM?Key=d6d4ac4e2c084ba78dc472e893d68e77&SIGUN_NM=시흥시

여기서 Key값은 사용자가 로그인하여 토큰 신청을 하면 데이터 포탈에서 토큰키값을 준다
그것을 url에 넣고 자신이 원하는 데이터를 뒤에다 적으면 된다

나는 시흥시에 있는 병원만 가져오고 싶어서 SIGUN_NM=시흥시로 설정했다

보통 자신이 원하는 데이터를 얻을때 써야되는 것들은 공공데이터 포탈에 적혀져 있다.

그런 다음 파이썬을 통해 url을 GET하고 그 데이터를 xml이나 json 형태로 받아오면 된다

```
import requests
import xml.etree.ElementTree as ET

    url = "https://openapi.gg.go.kr/GgHosptlM?Key=d6d4ac4e2c084ba78dc472e893d68e77&SIGUN_NM=시흥시"
    r = requests.get(url)
    print(r.text)
```

json 형태로 받으려면 뒤에 .json()을 붙이면 된다

# postman 활용

url을 입력했을때 데이터가 잘 들어오는지 보기 위해서는 전에 썼던 포스트맨 쓰는법 글을 읽어보면 좋을거같다.
