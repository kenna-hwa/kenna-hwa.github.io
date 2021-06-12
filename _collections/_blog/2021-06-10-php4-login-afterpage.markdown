---
layout: post
title:  "[PHP] 로그인 전,후 페이지 만들기"
author: Kenna
date:   2021-06-10 20:26:35 +0830
image: https://images.unsplash.com/photo-1611647832580-377268dba7cb?ixid=MnwxMjA3fDB8MHxzZWFyY2h8OHx8cGhwfGVufDB8fDB8fA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60
rating: 16
description: 수업 복습
categories : PHP
tags: PHP
---

###### PHP
[PHP 공식 홈페이지]("https://www.php.net/")

###### index.php 페이지에서 로그인 전/후 페이지 만들기


index.php의 로그인/회원가입 링크를 로그인 후에는<br>
로그아웃/회원정보 페이지로 변경되도록 조건문을 이용한다.

1. 로그인 전 (로그인/회원가입)
2. 로그인 후 (로그아웃/회원정보)

1번과 2번을 구분하는 조건은 <br>
세션이 있냐 없냐로 구분할 수 있다.

index.php 상단에 세션 사용 코드를 넣는다.


<pre>
< ? php

session_start();

? >
</pre>

세션값이 들어와 있으면 로그인 상태(아이디, 비밀번호 검증이 끝남-회원임) 이고 세션값이 없으면 로그인이 안된 상태다.

<pre>

만약에   세션값이 없다면    로그인/회원가입 링크
if     (  ! $s_id)  )     {

    echo "
    < p>
    < a href=\"login/login.php\">로그인< /a>
    < a href=\"members/join.php\">회원가입< /a>
    </ p>; 
    ";

    아니면 (세션값이 있다면)  로그아웃/회원정보 링크
} else {

    echo "
    < p>
    < a href=\"login/logout.php\">로그아웃< /a>
    < a href=\"members/edit.php\">회원정보< /a>
    < /p>;
    ";
};

</pre>

<br>
이것을 아래와 같이 표현할 수 있다.
<br>

<pre>


< ? php
   // 로그아웃 상태
    if(!$s_id){
? >

    < p>
    < a href="login/login.php">로그인< /a>
    < a href="members/join.php">회원가입< /a>
    < /p>

< ? php } else {
    // 로그인이 되었다면 
? >

    < p>
       <? php echo $s_name; ?>님 안녕하세요.
    < /p>
    < p>
    < a href="login/logout.php">로그아웃< /a>
    < a href="members/edit.php">회원정보< /a>
    < /p>

< ? php
    };
? >    

</pre>

<br>

###### 세션 변수가 없으면 없다고 말하기

**삼항연산자 이용**
<br>

이거? 맞으면이거 : 아니면이거;

<pre>

< ? php

$s_id = isset($_SESSION["s_id"])? $_SESSION["s_id"] : ""; 

$s_name = isset($_SESSION["s_name"])? $_SESSION["s_name"] : ""; 

//null이 아니면 "" 빈 값

? >

</pre>

**isset()**<br>

isset 함수는 변수가 설정되었는지 확인하는 함수.
변수가 선언되어야하고 Null값이 아닌지 확인한다.
변수가 선언되어 있으면 true, 비어있으면 False

