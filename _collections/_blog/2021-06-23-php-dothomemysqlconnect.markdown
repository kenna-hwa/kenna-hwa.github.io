---
layout: post
title:  "[PHP] Dothome 계정 MySQL 연결하기"
author: Kenna
date:   2021-06-23 12:26:35 +0830
image: https://images.unsplash.com/photo-1611647832580-377268dba7cb?ixid=MnwxMjA3fDB8MHxzZWFyY2h8OHx8cGhwfGVufDB8fDB8fA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60
rating: 30
description: 개인 포트폴리오 작업
categories : PHP
tags: PHP
---

###### PHP
[Dothome]("https://www.dothome.co.kr/index.php")


###### Dothome

닷홈 계정에 닷홈에서 제공한 DB 연결하기

<br>

**닷홈 계정 만들고 phpmyadmin 접속**<br>

닷홈 가입하고 마이닷홈-상세보기 하단에  
MySQL 관리 주소가 보인다.  
'개인아이디.dothome.co.kr/myadmin' 로 접속 가능   

   
<br>

**phpmyadmin에서 DB와 테이블 생성**<br>

phpmyadmin에서 쿼리나 GUI를 이용해서 데이터베이스와 테이블을 만든다.   
**내 생각엔 무료 호스팅이라 기본 DB 말고는 추가 제공하지 않는 것 같다. 데이터베이스 추가하려고 하면 권한없음으로 뜸**  
<br>

테이블에 데이터를 추가한다.  
  

<br>

**dbcon.php 파일 작성하기**

로컬에서 작성중인 php 파일들에 연결할  
dbcon.php 파일을 작성한다.  

<br>

<pre>


< ?php

//DB 연결
$dbcon = mysqli_connect("localhost", "DB아이디", "DB비밀번호", "데이터베이스명") or die("DB 접속 실패");
mysqli_set_charset($dbcon, "utf8");

? >
</pre>

localhost는 localhost다.  

<br>

**FTP로 업로드**<br>

FTP로 업로드 시킨 후 확인한다.
<br>