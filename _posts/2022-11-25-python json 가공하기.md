---
layout: single
title: "json 가공하기"
toc: true
toc_sticky: true
toc_label: "목차"
categories: python
toc_icon: "bars"
tags: [python]
---

📘파이썬

# XML 파싱
Python json 형태로 XML 파싱하는 xmltodict 라이브를 써야한다
> pip install xmltodict

그 다음 자신이 원하는 데이터를 request 받고
>req = requests.get(apiUrl)

xml형식으로 바꿔준다
>xpars = xmltodict.parse(req.text)

# str ,dict 형식으로 바꾸기
json 형식의 str으로 바꿔준다.
> jsonDump = json.dumps(xpars)

바꿔준 json 형식의 str을 dict형식으로 바꾼다
> jsonBody = json.loads(jsonDump)

자신이 원하는 키 값을 보는 방법은?
> 
> keys = [key for key in jsonBody['GgHosptlM']]
>
> print (keys)

# 자신이 원하는 내용으로 바꾸기
```
// row키값의 배열들중 0~72까지 자신이 필요없는 부분 del를 이용하여 삭제
jsonBody2 = jsonBody ['GgHosptlM']['row']
print(type(jsonBody2))
for x in range (0,72):
    del jsonBody2[x]['SIGUN_CD']
    del jsonBody2[x]["LICENSG_DE"]
    del jsonBody2[x]["LICENSG_CANCL_DE"]
    del jsonBody2[x]["BSN_STATE_DIV_CD"]
    del jsonBody2[x]["UNITY_BSN_STATE_DIV_CD"]
    del jsonBody2[x]["UNITY_BSN_STATE_NM"]
    ...

```
# json 파일로 저장하기
```
with open("./test.json",'w',encoding='utf-8')as file:
    json.dump(jsonBody2,file,indent="\t",ensure_ascii=False)
    
```