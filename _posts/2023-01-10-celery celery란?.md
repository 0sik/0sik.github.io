---
layout: single
title: "celery๋?"
toc: true
toc_sticky: true
toc_label: "๋ชฉ์ฐจ"
categories: celery
toc_icon: "bars"
tags: [celery]
---

๐celery

# worker

- ์ฑ๊ธ์ค๋ ๋ ๊ธฐ๋ฐ์ผ๋ก ์๋ํ๋ javascript๋ ์ฑ๊ธ์ค๋ ๋์ ๋จ์ ์ ๋ณด์ํ๊ธฐ ์ํด ์ฝ๋๋ค์ด ๋น๋๊ธฐ๋ก ์คํ๋๋ค. 
๊ทธ๋ฌ๋ API๋น๋๊ธฐ ์คํ์ด ๋๋ฌด ๋ง์ด ์์ด๊ฒ ๋๋ฉด ๋ชจ๋  ์์์ ์คํ ์๋๊ฐ ๋๋ ค์ง ์ ์๋ค.
์ด ๋ฌธ์ ๋ฅผ ํด๊ฒฐํ๊ธฐ ์ํด ๋์จ ๊ฒ์ด ๋ฐ๋ก ์์ปค(Worker) ์ด๋ค. ์น ์์ปค API๊ฐ ๋ฉํฐ ์ค๋ ๋ฉ์ ์ง์ํ๊ฒ ๋์ด ์์ปค๋ฅผ
์ด์ฉํ๋ฉด ์์ปค์์ ์์ฑ๋ ์คํฌ๋ฆฝํธ๋ ๋ฉ์ธ ์ค๋ ๋์์ ๋ถ๊ธฐ๋์ด ๋๋ฆฝ๋ ์ค๋ ๋๋ก ์คํ๋๊ธฐ ๋๋ฌธ์ ๋ฉ๋ชจ๋ฆฌ ์์์ ํจ์จ์ ์ผ๋ก ์ฌ์ฉํ  ์ ์๋ค.


- Celery๋ Python์ผ๋ก ์์ฑ๋ ๋น๋๊ธฐ ์์ ํ(Asynchronous task queue/job queue)์๋๋ค. ์์ ์๊ฐํ ์์(Task)๋ฅผ 
๋ธ๋ก์ปค(Broker, ์คํฌ์นด ์๋ฒ๋ Redis๋ฅผ ์ฌ์ฉ)๋ฅผ ํตํด ์ ๋ฌํ๋ฉด ํ๋ ์ด์์ ์์ปค(Worker)๊ฐ ์ด๋ฅผ ์ฒ๋ฆฌํ๋ ๊ตฌ์กฐ์๋๋ค. 
ํฌ์ธํธ ์ ๋ฆฝ-๊ณต์ ์ ๋ฐ๋ฅธ ๋ถ๋ฐฐ์ฒ๋ฆฌ, ํฌ์คํ ๊ธฐ๋ฅ, ํ์ด์ค๋ถ/ํธ์ํฐ ๊ณต์ ๋ฑ์ ๋น๋๊ธฐ ์ฒ๋ฆฌ๊ฐ ํ์ํ ์์์ Celery์ ์์ํ์ฌ ์ฒ๋ฆฌํ๊ณ  ์์ต๋๋ค.



# Celey
- ์ฌ์ฉ์์๊ฒ ์ฆ๊ฐ์ ์ธ ๋ฐ์์ ๋ณด์ฌ์ค ํ์๊ฐ ์๋ ์์๋ค๋ก ์ธํด ์ฌ์ฉ์๊ฐ ๋๋ผ๋ Deley
  ๋ฅผ ์ต์ํ ํ๊ธฐ ์ํด ์ฌ์ฉ ๋๋ค.

- Celery๋ task๋ฅผ broker๋ฅผ ํตํด ์ ๋ฌํ๊ณ  worker๊ฐ ์ฒ๋ฆฌํ๋ ๊ตฌ์กฐ์๋๋ค.

- ์ฅ๊ณ ์์ ๋ฐ์ํ ์์ฒญ์ message broker๊ฐ ๋ฐ์ ์์ปค(celery)๋ฅผ ์ด์ฉํ์ฌ ๋ถ์ฐ์ฒ๋ฆฌํ๋ค


## Celery ๋์๊ตฌ์กฐ
  ![Bar](/assets/img/celery.png)

-Celery์ ๋์ ๊ตฌ์กฐ์ด๋ค. ์น ์๋น์ค(Django)์์ ๋ฐ์ํ ์์ฒญ(Task)๋ฅผ Message Broker์์ ๋ฐ์ 
Celery๋ฅผ ์ด์ฉํ์ฌ ๋ถ์ฐ ์ฒ๋ฆฌ๋ฅผ ์งํํ๋ค. Celery์์๋ ์์์ด ์๋ฃ๋๋ (ํน์  ์ด๋ฒคํธ)์ DB Task๋ฅผ ์ํํ๋ค.

## Celery ์ฐ๋์ด์ 

- ์๋ฅผ ๋ค์ด ํ์ ๊ฐ์ ์ถํ ์ด๋ฉ์ผ ๋ฐ์ก, ์ด๋๋ฏผ ์ฃผ๋ฌธ๋ด์ญ ์์ ๋ค์ด๋ก๋ ๊ฐ์ ๊ธฐ๋ฅ์ด ํด๋น๋๋ค.
์ด API ์ ํฌํจ๋ ์ธ๋ถ ์ฐ๋์ด๋ ๋ฌด๊ฑฐ์ด ์์๋ค์ Celery Task๋ก ์ ์ํด์ ๋ธ๋ก์ปค(RabbitMQ)์ ์ปจ์๋จธ(Celery Worker)๋ฅผ 
์ด์ฉํด ๋น๋๊ธฐ๋ก ์ฒ๋ฆฌํจ์ผ๋ก์จ ์ฌ์ฉ์์๊ฒ ๊ฐ๋ฅํ ๋น ๋ฅธ ์๋ต ๊ฒฐ๊ณผ๋ฅผ ์ ๊ณตํ  ์ ์์ ๊ฒ์ด๋ค.

## ์์ ๊ฒฐ๊ณผ ๋ณด๊ดํ๊ธฐ (Result Backend)

- Celery๋ Task ์์ ๊ฒฐ๊ณผ๋ฅผ ์ ์ฅํ๊ธฐ ์ํ ์ฌ๋ฌ๊ฐ์ง result backend ๋ฅผ ๋ด์ฅํ๊ณ  ์๋ค.
(์: SQLAlchemy, Django, Memcached, RabbitMq, Redis, RPC ๋ฑ๋ฑ) 
result backend ๋ฅผ ์ง์ ํ๋ ค๋ฉด Celery ์ธ์คํด์ค์ backend ํค์๋ ์ธ์๋ฅผ ์ถ๊ฐํ๋ค.
rpc ๋ฅผ result backend ๋ก ์ง์ ํ  ๊ฒฝ์ฐ ์์ ๊ฒฐ๊ณผ๋ฅผ ์์ AMQP ๋ฉ์์ง๋ก ๋ค์ ๋๋ ค๋ณด๋ด๋ ๋ฐฉ์์ผ๋ก ๋์ํ๊ณ , 
์์ ๊ฒฐ๊ณผ๋ก ๋ฐํ๋ AsyncResult ์ธ์คํด์ค๋ฅผ ์ ์งํ  ์ ์๊ฒ ๋๋ค.


## celery ์ค์ 
1. celery.py
  celery.py ์์ app =Celery(ํ์ผ์ด๋ฆ,broker=๋ธ๋ก์ปค์ค,backend=๋ฐฑ์๋์ค,include=```[ํ์ผ์ด๋ฆ.tasks]```)
2. ```@app.task```
  - tasts.pyํ์ผ์์ ```@app.task```๋ฐ์ ํจ์ ๊ตฌํ
3. ํด๋น ํ์ผ์์ ์ธ๋ถ๋ถ์  ๊ตฌํํํจ์.deley

์์ฝํด์ ์ด๊ฒ์ด๋ฏ๋ก ๊น์์ ์ฝ๋ ์ฐธ๊ณ ํ ๊ฒ
## Celery ์์ปค ์คํ๋ฒ 

celery -A (ํ์ผ์ด๋ฆ) worker --loglevel=info