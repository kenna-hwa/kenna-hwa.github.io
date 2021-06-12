---
layout: post
title:  "[PHP] PHP 회원정보 수정 페이지 만들기"
author: Kenna
date:   2021-06-12 12:26:35 +0830
image: https://images.unsplash.com/photo-1611647832580-377268dba7cb?ixid=MnwxMjA3fDB8MHxzZWFyY2h8OHx8cGhwfGVufDB8fDB8fA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60
rating: 19
description: 수업 복습
categories : PHP
tags: PHP
---

###### PHP
[PHP 공식 홈페이지]("https://www.php.net/")


###### 회원정보 수정 edit.php 페이지 만들기

회원정보 수정 페이지는 회원 정보 입력 페이지와 모양은 같다. 
다만 일반적으로 수정이 가능한 정보와 불가능한 정보가 있기 떄문에 수정이 불가능한 정보는 데이터를 받아와서 출력만 해주고 수정이 가능한 정보는 **'update'** 쿼리를 이용해 덮어쓰기 해준다.

<br>
<br>

**회원정보 수정 페이지 만들기**
<br>

회원가입 페이지를 그대로 가져와서 **수정하지 않을 부분**인 이름, 아이디, 약관동의 부분은 input 태그를 뺀다.

<br>
이름, 아이디에는 기존 입력한 정보를 출력할 수 있도록 echo로 기존 정보를 받아온다.
<br>

비밀번호는 기존 정보를 노출하면 보안상 문제가 될 수 있으므로 join.php와 동일하게 둔다.

<br>
나머지 정보들은 기존 정보를 input 에 그대로 출력해야하므로 input 태그에 value 속성 값으로 < ?php echo $가져올컬럼의변수 ?>를 넣는다.

위 작업은 데이터베이스에서 기존 값을 가지고 오는 코드 작성 후에 진행해도 된다.

form태그의 action 값에는 edit_ok.php 를 설정해 edit_ok.php에서 수정된 정보를 데이터베이스로 보내는 작업을 한다.
<br><br>

**세션 연결하기**
<br>

당연하지만 회원정보를 수정하기 위해서는 로그인 검증을 거친 회원이어야 한다. 따라서 회원정보 페이지에서도 **세션** 을 가지고 있어야한다.

<br>
<pre>
< ?php

session_start();
$s_idx = isset($_SESSION[" s_idx"])? $_SESSION[" s_idx"] : ""; 

? >
</pre>
<br>

아래 코드는 혹시 세션이 없이 진입했는지 아닌지 확인하면서, 세션값이 없으면 오류 메세지를 출력하지 말라는 삼항연산자다.

**데이터베이스에서 기존 정보 받아오기**
<br>

데이터베이스에서 기존 정보를 받아오려면 우선 데이터베이스에 연결되어 있어야 한다.

외부파일 **include**를 한다.

<br>
<pre>
< ?php

include "../inc/dbcon.php";

?>
</pre>
<br>

**데이터베이스에  보낼 쿼리를 작성**
<br>

우선 작성할 것은 페이지에 노출해야 할 기존 정보들을 부르는 select문을 작성한다.

<pre>
< ?php 

$sql = "select * from members where idx='$s_idx';";

?>
</pre>

위 쿼리는 가입된 회원 정보가 들어있는 members 테이블에 세션값인 s_idx 번호의 정보값을 전부 가져오는 문장이다.

위 쿼리를 데이터베이스에 날리는 함수는 다음과 같다.

<pre>
< ?php 

$result = mysqli_query($dbcon, $sql);

? >
</pre>
<br>

위와 같은 쿼리를 보내고 값을 받아 오는 함수 중 사용이 편하도록 **컬럼명**으로 가져오는 **mysqli_fetch_array**를 사용한다.
<br>

<pre>
< ?php 

$array = mysqli_fetch_array($result); 

?>
</pre>
<br>
변수 $array로 넣어 각 값을 컬럼명으로 가져올 수 있다.
<br>
<br>

필요한 경우 date 타입으로 들어가 있는 생년월일에 대한 값을 **str_replace()** 함수로 바꿔 가져올 수 있다.
<br><br>

**str_replace("어떤 문자를", "어떤 문자로", "어떤 문장에서");**
<br>

<pre>
< ?php
         
    $birth = $array["birth"];
    $bitrh = str_replace("-", "", $birth);

?>
</pre>

<br><br>

**버튼 생성**
<br>

정보 수정 페이지에서 필요한 돌아가기, 정보수정, 회원탈퇴 세 개의 버튼을 만든다.

<br>

**돌아가기** 버튼은 button 타입은 button으로 onclick 이벤트 리스너에 location="index파일 경로" 혹은 이동하고 싶은 경로를 설정한다.
뒤로 가고 싶으면 history.go(-1) 함수를 설정해 한 페이지 뒤로가기를 설정할 수도 있다.

별도로 js파일에 함수를 만들어서 onclick으로 넣을 수도 있다.

<br>

**정보수정** 버튼은 button 타입은 submit으로 하고 form 태그에 onsubmit 이벤트 리스너로 스트립트를 걸어둔다.
스크립트가 필요한 이유는 필수 입력해야 하는 부분이 입력값을 넣지 않은 부분이 있는지, 조건에 맞지 않는 값을 넣지는 않았는지 검증하기 위해서다.
회원 가입 시 제시한 조건과 동일한 유효성 검사 코드를 이용해서 검사를 진행하고 action 값으로 설정된 php 파일을 통해 데이터베이스에 전달할 수 있도록 한다.

<br>

**회원탈퇴** 버튼은 회원 탈퇴를 하기 위한 페이지를 만들어서 클릭 시 해당 페이지로 진입할 수 있도록 한다.
onclick 이벤트 리스너에 페이지로 이동하는 js함수를 연결시킨다.

###### edit_ok.php 페이지 만들기


###### 회원탈퇴 delete.php 페이지 만들기


