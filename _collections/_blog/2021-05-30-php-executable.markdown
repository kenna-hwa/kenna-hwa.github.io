---
layout: post
title:  "[PHP] PHP executable not found"
author: Kenna
date:   2021-05-30 11:26:35 +0830
image: https://images.unsplash.com/photo-1606166245039-ffeba59d83a4?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1284&q=80
rating: 13
description: 오류 문제 해결
---

###### VScode 에서 오류 발생했을 때 해결하기

msg : PHP executable not found. Install PHP 7 and add it to your PATH or set the php.executablePath setting

###### 1) 환경변수 셋팅

순서
작업표시줄에서 찾기 > 설정 > 고급 시스템 설정 보기 검색 > 클릭 > 고급 > 하단에 환경 변수 > 시스템 변수 스크롤 내려서 Path 찾기

환경 변수 편집에 PHP경로가 삽입되어있는지 확인
없으면 Bitnami 폴더나 각자 설치한 php 폴더 찾아서 경로 복사
(속성에서 위치 확인한 후 \php 뒤에 붙임)

환경 변수 편집 Path에서 새로만들기 - 경로 붙여넣기 - 엔터 - 모두 확인 클릭

###### 2) VScode 에서 셋팅

VScode 왼쪽 아래 톱니바퀴 설정 > 설정 클릭 > 왼쪽 아래 확장 클릭
확장에서 PHP 찾기
PHP › Validate: Executable Path PHP 실행 파일을 가리킵니다. 아래의 
**Setting.json에서 편집** 찾아서 클릭

Setting.json의 가장 바깥 중괄호에
**"php executablePath" : "php실행파일(.exe) 경로"**,
**"php.validate.executablePath" : "php실행파일(.exe) 경로"**
두개를 넣고 저장 (필요시 문장 각각 뒤에 쉼표 붙임)

**여기서 그냥 속성에서 위치 확인한 것처럼 \ 한개씩만 붙이면 이스케이프 문자로 해석해서 적용이 안되니 C:\\Bitnami\\ 이런식으로 적어줘야 함**

저장하고 
VScode 재실행하면 끝!