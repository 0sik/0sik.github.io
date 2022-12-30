---
layout: single
title: "git 기본 사용법"
toc: true
toc_sticky: true
toc_label: "목차"
categories: github
toc_icon: "bars"
tags: [github]
---

📘github

# 리눅스 명령어
ls - 현재 위치의 파일 목록 조회
cd - change directory
mkdir - make directory
rmdir - 디렉터리 삭제
touch - 파일 생성
rm - 파일 삭제
cp - 파일 복사 
open - 파일 열기
code .-현재 위치에서 vscode열기

# 깃 기본 사용법

## 깃 기본 명령어
> git status : 현재 상태 확인
> git reset Head^ : 꺽쇠 수만큼 이전으로 돌아가게 하는 명령 , ^(한단계 앞) ^^(두단계 앞)
> git remote add origin github 주소 :github 주소와 연결
> git remote -v : 현재 연결된 저장소가 있는지 확인

## 깃허브에서 파일 가져오기
1. git pull : 원격저장소에 있는 프로젝트의 변경사항을 그대로 로컬저장소에 옮겨와 자동으로 병합
   - ```git pull origin master = git pull [원격 저장소의 이름] [원격 저장소에서 받아오고자 하는 브랜치의 이름]```
2. git clone 주소 : 원격저장소의 내용을 새로운 폴더에 그대로 복사하는 것

## 깃허브에 파일 올리기

1. git init(맨처음에만 설정) : 현재 폴더를 기준 폴더로 하고 git을 관리(해당 폴더를 git 로컬 저장소로 설정하는 명령어라 생각)
2. git add . : 로컬 저장소의 파일을 1차로 가상공간에 추가하는 명령어 "."은 모든 파일 업로드
3. git commit -m "메세지" : git commit -m 은 가상공간에 최종 저장
4. git push origin sub
  - 원격저장소로 최종 업로드 , origin은 원격저장소의 주소라고 생각
  - 뒤에 sub은 브랜치이다 main을 sub로 바꾸면 main 브랜치는 가만히 있고 , sub브랜치에 저장된다
  - 브랜치를 나눠서 관리하지 않으면 git push origin main




