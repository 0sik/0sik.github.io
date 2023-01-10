---
layout: single
title: "docker란무엇이며 쓰는법"
toc: true
toc_sticky: true
toc_label: "목차"
categories: docker
toc_icon: "bars"
tags: [docker]
---

📘docker

# Docker란
어플리케이션을 패키징 할 수있는 툴
개발자들의 pc마다 서버마다 서버 버전등 다르기때문에 
리눅스 컨테이너를 만들고, 사용할 수 있는 컨테이너화 기술

1. 원하는 개발 환경을 파일에 저장하면 , docker는 이를 원하는 어떤 머신에든 해당 환경을 시뮬레이션 해준다
2. 이러한 환경들은 각기 독립적으로 존재하기 때문에 , 원하는 환경이든 모듈식으로 관리 가능

## Docker의 장점

> 팀워크에서의 이점

개발을 하다보면 팀원들과 언어나 프레임워크의 버전이 달라 오류가 나는 경우가 있을 수 있다. 필자의 경우 프로젝트를 할 때 팀원들과 파이썬 버전이 달라서 이슈를 겪었던 적이 있다.

도커를 사용하면 이런 문제를 쉽게 해결할 수 있다. 도커 이미지에 언어나 프레임워크 버전을 미리 모두 정해놓을 수 있고 해당 이미지를 컨테이너화 시키면 그 컨테이너는 로컬 환경의 간섭 없이 독립적으로 구동하기 때문에 위와 같은 걱정을 할 필요가 싹 사라진다.

또한 Dockerfile을 사용하면 설치할 언어, 프레임워크, 패키지 등을 미리 코드 형태로 명시하고 어느 컴퓨터에서든 쉽게 자동으로 설치할 수 있다.

## Dockerfile
컨테이너를 어떻게 만들어야 되는지 설명서와 같은것이다
어플리케이션을 만드려면 필요한 파일이 무엇인지 어떤 프레임워크나 라이브러리를 설치해야하는지
환경변수 설정 , 스크립트 포함
copy files, install dependecies , set environment variables , run setup scripts

## DockerImage
실행되고 있는 어플리케이션 상태를 사진처럼 찍는다고 생각하면 편하다
변경이 불가능한 상태로 내가 지금 가지고있는 어플리케이션을 그대로 저장

## Docker Container
우리가 잘 캡쳐해둔 어플리케이션 이미지를 실행할 수 있는 것
우리가 준비한 어플리케이션을 찍은 iamge를 구동하는것

## 이미지 공유 방법
1. dockerfile작성한다음 image를 만든다
2. image를 container registry로 push
3. 서버에서 pull
4. 서버에서 run

# 도커 쓰기

## 이미지를 통해 컨테이너 실행 
> docker run --name 컨테이너 이름 -dit -p 8088:80 이미지 이름

nginx는 도커허브에 공용으로 쓰는 이미지라 바로 컨테이너가 띄어짐
공용이 아닌 개인 이미지면 자신의 도커 데스크탑에 이미지를 저장해야됨

## 도커 이미지 만들기
Dockerfile을 통해 도커 이미지 만들기
> docker build -t 이미지이름 .

## 도커허브에 이미지 올리기
> docker push 이미지이름

## 도커 컴포즈
일반적인 시스템은 단일이 아니다 여러 개의 어플리케이션이 서로 의존성 있게 구성되어 시스템이 이루어져있다
이때 필요한 기술이 도커 컴포즈이다.
> docker-compose.yml
```
  version: "3"
  services:
    compose1:
      build:
        comtext: ./compose1
       ports:
        - 8010:10
    compose2:
      build:
        comtext: ./compose2
       ports:
        - 8011:10        
```