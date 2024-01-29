---
layout: single
title: "워너플라이 (WANNAFLY)"
toc: true
toc_sticky: true
toc_label: "목차"
categories: project
toc_icon: "bars"
tags: [project]
---
📘 워너플라이 (WANNAFLY)

큐시즘이라는 동아리에서 만든 프로젝트 한 번에 지원서를 관리하고 작성하는 웹사이트 서비스 wannafly이다.
지금까지 한 프로젝트중 백엔드 부분에서 가장 잘하는 사람과 했던 프로젝트라고 생각하고,
정말 잘하는 사람과 프로젝트를 해서 그런지 인프라나 코드 리팩토링 코드리뷰등 정말 많은 것을 배운 기회였다.
다른 프로젝트와는 다른 이점들을 살펴보자.

# Lambda
Lambda를 이용하여 파이썬 맞춤법 검사기 라이브러리 사용, 하나의 작은 API를 사용하기 위해 EC2를 올리는게 비효율적, 람다를 사용하여 인프라 관리 부담 감소하게되었다.

처음에는 Docker을 활용하여 ec2에 플라스크 서버를 열어 스프링이랑 통신을 하려고 했다. 하지만 하나의 작은 api를 사용하기 위해 ec2에 올리는게 비효율적이라고 판단하여 aws lambda를 사용하게 되었다.

# JWT
JWT를 사용하면서 Refresh Token을 캐싱, 그 이유는 Access Token의 시간을 짧게 두어 Access Token을 탈취 당했을때를 대비, 로그인이 자주 풀리는 사용자 경험을 개선한다.

같이 프로젝트 하는 형이 설명해주었는데 학교 eclass만 가봐도 사용자가 로그인을 했을때 몇분 지나지 않아서 로그인이 풀리는 경우가 존재한다.
그 경험을 개선하고자 refresh token을 사용하였다. 

이점들은 여기까지 인거같고, 하지만 이 프로젝트에서는 코드적는 부분이나 스프링에 전체적인 틀 객체지향 생활체조 원칙을 지키며 코딩하고 여러가지로 많이 배운 프로젝트였다.