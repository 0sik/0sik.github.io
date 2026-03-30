---
layout: single
title: "github협업"
toc: true
toc_sticky: true
toc_label: "목차"
categories: github
toc_icon: "bars"
tags: [github]
---

📘github

<!-- 깃협업 forking 개념 https://gmlwjd9405.github.io/2017/10/28/how-to-collaborate-on-GitHub-2.html --> 
<!-- 커밋 템플릿 만들기 https://kkangsg.tistory.com/95 -->

# Forking Workflow
모든 프로젝트 참여자는 로컬 저장소와 자신의 원격 저장소를 각각 가진다.
프로젝트는 Organization이 관리하는 중앙 원격 저장소를 기준으로 운영되며, 참여자는 중앙 저장소를 직접 수정하지 않고 중앙 저장소를 fork한 자신의 원격 저장소에서 작업한다.
이후 변경 사항은 자신의 원격 저장소에 push한 뒤, Pull Request를 통해 중앙 원격 저장소에 반영한다.
즉, 모든 개발자가 하나의 중앙 저장소에 직접 push하는 방식이 아니라, 각자 자신의 원격 저장소를 거쳐 기여하고, 프로젝트 관리자 또는 권한을 가진 관리자가 이를 검토한 뒤 중앙 저장소에 병합하는 방식이다.

중앙 원격 저장소: 프로젝트 관리자 또는 조직이 관리하는 기준 저장소
개인 원격 저장소: 중앙 저장소를 fork하여 GitHub 상에서 관리하는 개인 저장소
로컬 저장소: 개인 PC에 clone하여 사용하는 작업용 저장소

# 사용 방법

## 1. 중앙원격저장소를 포크해서 자신만의 원격 저장소를 만든다

## 2. 원격저장소에서 자신의 로컬 저장소로 clone을 한다
> git clone 원격저장소 url

## 3. 중앙 원격 저장소를 연결한다
> git remote add upstream 중앙원격저장소 url
이렇게 연결하면 로컬저장소를 프로젝트 중앙 원격 저장소와 같은 상태로 유지할 수 있다.

## 4. 현재 로컬에서 작업중인 branch 위치 표시
> git checkout -b "branch name"
"branch name"으로 브랜치를 바꾸고 없으면 생성한다

## 5. 로컬 저장소의 파일을 1차로 가상공간에 추가한다
> add .

## 6. 가상공간에 최종 저장
> git commit

## 7. 원격저장소(origin)에  푸시
> git push origin branch name

## 8. 중앙 원격 저장소로 pull request 검사받기
> git hub 홈페이지에서 pull request누르기

## 9.팀원들이 다 확인했으면 merge(병합)
> 병합누르고 브랜치 삭제하고 싶으면 삭제 누르면 됨


## 중앙 원격 저장소의 코드베이스에 새로운 커밋이 있다면 
> git pull upstream main 로 가져온다
