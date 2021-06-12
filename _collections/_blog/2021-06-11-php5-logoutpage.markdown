---
layout: post
title:  "[PHP] PHP 로그아웃 페이지 만들기"
author: Kenna
date:   2021-06-11 17:26:35 +0830
image: https://images.unsplash.com/photo-1611647832580-377268dba7cb?ixid=MnwxMjA3fDB8MHxzZWFyY2h8OHx8cGhwfGVufDB8fDB8fA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60
rating: 17
description: 수업 복습
categories : PHP
tags: PHP
---

###### PHP
[PHP 공식 홈페이지]("https://www.php.net/")

###### logout.php 페이지 만들기

로그인은 **Session세션** 을 생성할 수 있도록 사용자를 검증하고, 세션을 만드는 일이다.

세션을 가진 사용자는 회원 검증을 받은 사람이고(로그인 과정 통과)<br>
세션이 없는 사용자는 회원 검증이 안 된 사람이다.

<pre>

< ?php

//세션 시작

session_start();
$s_idx = isset($_SESSION["s_idx"])? $_SESSION["s_idx"] : ""; 
$s_name = isset($_SESSION["s_name"])? $_SESSION["s_name"] : ""; 
$s_id = isset($_SESSION["s_id"])? $_SESSION["s_id"] : ""; 

? >

</pre>


따라서 세션이 있는 사용자에게서 세션을 삭제하게 할 수 있게 해주면 그것이 **로그아웃**기능이다.<br><br>



logout.php 페이지를 만들고
세션을 사용할 수 있도록 **세션 스타트 함수**를 넣는다.
<br><br>
<pre>
< ?php

session_start();

? >
</pre>
<br>
**세션 삭제 함수**를 넣는다.

**unset();** 
<br><br>
<pre>
< ?php

unset($_SESSION["세션으로 사용되는 변수"]);

? >
</pre>
<br>

세션 삭제를 완료하면 **로그아웃 완료 메세지**를 출력하고 페이지를 넘겨 세션이 삭제된 다른 페이지를 노출한다.
<br><br>
<pre>
< ?php
echo "

    < script type=\"text/javascript\">
    alert(\"로그아웃 되었습니다\");
    location.href=\"../index.php\";

    </ script> 
    
";
? >
</pre>

