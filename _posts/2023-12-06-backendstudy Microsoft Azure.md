---
layout: single
title: "Microsoft Azure"
toc: true
toc_sticky: true
toc_label: "목차"
categories: backendstudy
toc_icon: "bars"
tags: [backendstudy]
---
📘 Microsoft Azure

# Microsoft Azure
Microsoft Azure는 Microsoft에서 제공하는 클라우드 서비스입니다. Amazon의 AWS(Amazon Web Service)나 Google GCP(Google Cloud Platform)에 버금가는 인기 클라우드 서비스입니다.이 문서에서는 Microsoft Azure를 도입할 때의 이점과 이해하기 쉬운 유용한 정보를 설명합니다.

가입자는 이러한 서비스를 사용하여 가상 머신( VM ) 및 데이터베이스 와 같은 클라우드 기반 리소스를 생성할 수 있습니다

# Kubernetes
Kubernetes는 컨테이너화 된 애플리케이션의 자동 디플로이, 스케일링 등을 제공하는 관리시스템으로 오픈 소스 기반의 솔루션 입니다.

Microsoft Azure의 Kubernetes 서비스(AKS)를 사용하여 컨테이너화된 애플리케이션을 더 쉽게 배포하고 관리가 가능하며 Jenkins, Terraform 등의 오픈소스 도구를 활용하여 손쉽게 파이프라인을 추가 및 관리 할 수 있습니다. 이러한 특성으로 개발자의 운영에 대한 복잡성 및 관리에 대한 업무 부담을 감소시키고 마스터 노드에 대한 추가 비용이 발생하지 않아 효율적인 인력 및 비용 관리가 가능합니다. 

## Kubernetes 장점
1. 간편한 배포 및 관리
2. 안정적인 응용 프로그램 화갖ㅇ 및 실행
3. 오픈소스도구&api로 원하는 방식으로 작업
4. 몇번의 클릭만으로 ci/cd설정

# Kubernetes vs docker
컨테이너를 하나만 띄워서 사용해야지! => 도커
0월 0시에, 100개의 컨테이너를 자동으로 생성해야지! => 쿠버네티스
즉, 도커는 ’이미지를, 컨테이너에 띄우고 실행하는 기술’이고
쿠버네티스는 '도커를 관리하는 툴'이라고 생각하시면 됩니다.
따라서, 도커는 '한 개의 컨테이너를 관리’하는 데 최적화 되어있고,
쿠버네티스는 '여러 개의 컨테이너를, 서비스 단위로 관리’하는 데 최적화 되어있습니다.