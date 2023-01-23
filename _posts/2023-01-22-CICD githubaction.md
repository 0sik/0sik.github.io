---
layout: single
title: "CICD란?"
toc: true
toc_sticky: true
toc_label: "목차"
categories: cicd
toc_icon: "bars"
tags: [cicd]
---

📘CICD(github action)

# CICD 파이프라인

CI/CD 파이프라인은 새 버전의 소프트웨어를 제공하기 위해 수행해야 할 일련의 단계입니다. 지속적 통합/지속적 배포(CI/CD) 파이프라인은 DevOps 또는 사이트 신뢰성 엔지니어(SRE) 방식을 통해 더 효과적으로 소프트웨어를 제공하는 데 초점을 맞춘 방법입니다.

CI/CD 파이프라인은 특히 통합 및 테스트 단계와 제공 및 배포 단계에서 모니터링 및 자동화를 도입하여 애플리케이션 개발 프로세스를 개선합니다. CI/CD 파이프라인의 각 단계를 수동으로 실행할 수도 있지만, CI/CD 파이프라인의 진가는 자동화할 때 드러납니다.


## CICD파이프라인 단계
빌드->테스트->통합(지속적인 통합(CI))-> 배포 (지속적 배포(CD)

CI/CD 파이프라인의 단계는 각기 다른 태스크 하위 집합으로 이루어져 있는데, 이를 파이프라인 단계(pipeline stage)라고 부릅니다. 일반적인 파이프라인 단계는 다음과 같습니다.

빌드(Build) - 애플리케이션을 컴파일하는 단계
테스트(Test) - 코드를 테스트하는 단계. 이 단계를 자동화하여 시간과 수고를 줄일 수 있습니다.
릴리스(Release) - 애플리케이션을 리포지토리에 제공하는 단계
배포(Deploy) - 코드를 프로덕션에 배포하는 단계
검증 및 컴플라이언스(Validation & compliance) - 빌드 검증 단계는 해당 조직의 필요에 따라 결정됩니다. Clair와 같은 이미지 보안 스캔 툴을 사용하여 알려진 취약점(CVE)과 비교하는 방법으로 이미지의 품질을 보장할 수 있습니다.

## 종류 
1. github action
2. 젠킨스

# github action

소프트웨어 workflow를 자동화할 수 있도록 도와주는 도구

## github action 개념
1. Workflow
여러 Job으로 구성되고, Event에 의해 트리거될 수 있는 자동화된 프로세스
최상위 개념
Workflow 파일은 YAML으로 작성되고, Github Repository의 .github/workflows 폴더 아래에 저장됨

2. Event
Workflow를 Trigger(실행)하는 특정 활동이나 규칙
예를 들어 다음과 같은 상황을 사용할 수 있음
특정 브랜치로 Push하거나
특정 브랜치로 Pull Request하거나
특정 시간대에 반복(Cron)
Webhook을 사용해 외부 이벤트를 통해 실행

3. Job
Job은 여러 Step으로 구성되고, 가상 환경의 인스턴스에서 실행됨
다른 Job에 의존 관계를 가질 수 있고, 독립적으로 병렬 실행도 가능함

4. Step
Task들의 집합으로, 커맨드를 날리거나 action을 실행할 수 있음

5. Action
Workflow의 가장 작은 블럭(smallest portable building block)
Job을 만들기 위해 Step들을 연결할 수 있음
재사용이 가능한 컴포넌트
개인적으로 만든 Action을 사용할 수도 있고, Marketplace에 있는 공용 Action을 사용할 수도 있음

