---
layout: post
title:  "[Ruby] jekyll 블로그 설치를 위한 ruby 설치"
author: Kenna
date:   2021-10-18 13:26:35 +0830
image: https://images.unsplash.com/photo-1522776851755-3914469f0ca2?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1170&q=80
rating: 64
description: jekyll 블로그 설치를 위한 ruby 설치 과정 기록
categories : Ruby
tags: Ruby
---

###### jekyll 블로그 설치를 위한 ruby 설치 과정 기록

<br>

회사 노트북에서 지킬 블로그 번들을 하려니 루비를 설치해야 해서  


1) 우선 루비 설치

[루비 오피셜 다운로드]("https://rubyinstaller.org/downloads/")    
<br>

너무 높은 버전으로 설치하면 bundler 설치에서 에러가 나는 경우가 있다.  
이 글을 쓸 때는 Devkit 포함해서 3.0.2 버전이 릴리즈 되어 있었는데,  
번들러 오류가 나서 참고 블로그에서 말씀하신대로 **2.4.4.1 버전**으로 설치
PATH나 utf-8 같이 체크해야 하는 것들을 체크하고 설치해주었고  
msys64도 같이 설치했다. (나중에 혹시 사용할까봐)  

<br>
<br>

2) 루비를 통해 지킬 설치  

<br>

루비를 설치하고 루비 cmd를 이용해서 지킬을 설치한다.  
시작에서 **Start Command Prompt with Ruby** 를 검색한다.  
다른 블로그에서는 gemfile이 있는 곳에서 진행하면 된다고 했는데  
경로 찾을 필요 없이 Start Command ... 게 제일 정확한거 같다.    
그냥 cmd를 열면 경로 오류가 난다.  

<br>
<Br>

지킬을 위한 명령어는 다음과 같다.  

<br>

`gem install jekyll`  
`gem install minima`  
`gem install bundler`  
`gem install jekyll-feed`  
`gem install tzinfo-data`  
<br>
<br>


3) 지킬 테마 다운로드

<br>

["http://jekyllthemes.org/"]
["https://jamstackthemes.dev/ssg/jekyll/"]

다운받아 압축을 풀어준다.  



<br>
<br>

4) 지킬 bundle 실행
<br>

Start Command... 루비 콘솔창에서 블로그 저장 폴더로 이동하거나  
블로그 저장 폴더에서 powerShell 등을 실행해  
아래 명령어로 인코딩을 먼저 실행한다.  
`chcp 65001`  
그리고 지킬을 실행한다.  
`jekyll serve` 

로컬로 블로그를 확인 할 수 있다.  

<br>
<br>

