---
layout: post
title:  "[PHP] admin 페이지 만들기"
author: Kenna
date:   2021-06-15 21:26:35 +0830
image: https://images.unsplash.com/photo-1611647832580-377268dba7cb?ixid=MnwxMjA3fDB8MHxzZWFyY2h8OHx8cGhwfGVufDB8fDB8fA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60
rating: 25
description: 수업 복습
categories : PHP
tags: PHP
---

###### PHP
[PHP 공식 홈페이지]("https://www.php.net/")


###### 관리자 페이지 구조

관리자페이지에는 보통 회원관리, 게시판관리 기능이 있고  
관리자페이지에는 **권한**이 존재하기 때문에 메인 페이지에서부터 진입 링크를 별도로 관리하고 노출된 주소로 접속하더라도 로그인 된 관리자 권한이 없으면 이용하지 못하도록 별도의 세션 관리가 필요하다.  

<br>

또한 회원관리 페이지에서는 연결한 데이터베이스에서 회원정보 테이블을 가져와 테이블로 뿌려줘야 한다.  

<br>



관리자페이지 - 관리자 검증  
     └ 회원 관리 - 회원 정보 수정 / 회원 삭제 등
     └ 게시판 관리  
     .  
     .  
     .  

<br>
<br>

###### 관리자 세션 만들기

**index.php에서 보일 관리자페이지 링크 만들기**
<br>
<br>

index.php이 가지고 있는 세션 값으로 관리자가 로그인 한 경우에만 **'관리자페이지'** 가 노출 될 수 있도록 조건문 설정  
  
로그인 검증을 통과한 사람에게 보이는  
'로그아웃', '회원정보' 링크 옆에 '관리자페이지' 링크를 만든다.  

<pre>
< a href="admin/admin.php">관리자페이지 < /a>
</pre>

해당 a 태그는 관리자 아이디로 로그인했을 때만 보여야 하므로  
조건문으로 태그를 감싼다.  

<pre>
< ?php
   // 로그아웃 상태
    if(!$s_id){
? >
    < a href="login/login.php">로그인< /a>
    < a href="members/join.php">회원가입< /a>



< ?php 
    } else {    // 로그인이 되었다면 
? >

       < ?php echo $s_name; ? >님 안녕하세요.



< ?php
    //관리자페이지 링크 보이게 하기 
    if($s_id == "admin") {  //admin으로 로그인 했을때만 아래 링크가 보인다.
? >
    < a href="admin/admin.php">관리자페이지< /a>
< ?php 
    };    
? > //관리자페이지 링크 보이게 하기 끝


    < a  href="login/logout.php" title="로그아웃" onclick="log_out()">로그아웃< /a>
    < a href="members/edit.php">회원정보< /a>

< ?php
    };
? >    
</pre>


<br>
<br>

###### admin.php 만들기

별도의 php 파일을 만들고 페이지 구성을 넣는다.  
   

이 페이지는 반드시 admin으로 로그인한 관리자 권한만 볼 수 있도록
세션 session을 생성한다.  
이 세션 코드는 별도의 파일로 만들어 저장해두면  
추후 관리자가 추가되더라도 하나의 파일 수정으로 여러 개의 페이지를 관리할 수 있다.

<pre>
< ?php

session_start(); //세션 기능 시작
$s_id = isset($_SESSION["s_id"])? $_SESSION["s_id"]:"";
//$_SESSION["s_id"]로 받아온 세션의 아이디값이 있는지 확인하고 변수에 저장


//관리자 권한인 경우만 접속 가능 하도록 조건문 생성

if($s_id != "admin"){ 
    //받아온 세션의 아이디 값이 admin이 아니면 아래를 출력하고 스크립트로 링크를 이동시킴

    echo "
    < script type=\"text/javascript\">
    
    alert(\"관리자 권한이 필요합니다.\");
    location.href=\"../index.php\";
    
    < /script>
    
    
    ";
};

? >
</pre>

<br><br>

###### list.php 만들기

admin.php에서 넘어갈 수 있는 페이지 중 회원관리 페이지를 만든다.

페이지에 테이블 형태로 뿌려져야 하기 때문에 필요한 필드의 수 만큼 페이지를 만든다.  
가장 기초가 되는 테이블 구성은 아래와 같다.  
제목행 이후로 부터는 별도로 만들지 않아도 테이블에 정보가 뿌려지면서 자동으로 생성된다.  
수정과 삭제는 링크를 통해 각각 회원정보 수정 페이지와 회원 삭제 페이지로 연결될 수 있도록 한다.
    
<pre>
    < table>
        < tr>
            < td>회원번호< /td>
            < td>이름< /td>
            < td>아이디< /td>
            < td>전화번호< /td>
            < td>이메일< /td>
            < td>생일< /td>
            < td>주소< /td>
            < td>수정< /td>
            < td>삭제< /td>
        < tr>
    < /table>
</pre>

<br>

**1. 세션 삽입하기**

<br>

회원 리스트를 볼 수 있는 사람은 관리자 뿐이므로 관리자 권한을 확인하는 세션을 상단에 추가한다.

<pre>
< ?php

include "../admin_check.php"; //위에서 만든 파일
? >
</pre>

<br>

**2. 데이터베이스 연결**

<br>

회원 리스트는 연결된 데이터베이스에 저장되어 있기 때문에 데이터 베이스를 연결한다.

<pre>
< ?php

include "../../inc/dbcon.php"; //데이터베이스를 외부 파일로 연결한다

? >
</pre>

<br>

**3. 쿼리 작성/전송**

<br>

회원 리스트의 값을 화면에 출력해야 하기 때문에 SELECT문을 사용한다. 

<pre>
< ?php

include "../../inc/dbcon.php"; //데이터베이스를 외부 파일로 연결한다

? >
</pre>
  
회원정보를 가져올 쿼리를 작성한다.

<pre>
$ sql = "select * from members;";
//우선 다 가져오고 나서 컬럼 이름으로 하나씩 꺼내오면 된다.
//모든 회원의 정보가 다 나와야 하기 때문에 where 절은 사용하지 않는다.
</pre>
  
쿼리를 데이터베이스로 보낸다.
  
<pre>
$result = mysqli_query($dbcon, $sql);
</pre>
  
**4. 값 받아서 테이블에 뿌리기**
  
  <br>

받아온 값들은 세 가지 방법으로 가져올 수 있다.   
   
- mysqli_fetch_row();   
- mysqli_fetch_array();   
- mysqli_num_rows();  
   
여기서는 컬럼명이 명시된 것이 편하니 array 방식을 사용한다.  

<pre>
$array = mysqli_fetch_array($result);
</pre>
   
이렇게 가져온 값을 테이블에 $array[i] 로 넣는다.  
   


<pre>
    < table>
        < tr>
            < td><?php echo $array["회원번호"]; ?>< /td>
            < td><?php echo $array["아이디"]; ?>< /td>
            < td><?php echo $array["이름"]; ?>< /td>
            < td><?php echo $array["전화번호"]; ?>< /td>
            < td><?php echo $array["이메일"]; ?>< /td>
            < td><?php echo $array["생일"]; ?>< /td>
            < td><?php echo $array["주소"]; ?>< /td>
            < td>< a href="edit.php?g_idx=<?php echo $array["idx"]; ?>">수정< /a>< /td>
            < td>< a href="#" onclick='del_mem(<?php echo $array["idx"]; ?>)'>삭제< /a>< /td>
        < tr>
    < /table>
</pre>

   
그런데 이렇게만 넣으면 한 줄만 출력되게 된다.  
반복문을 사용해서 테이블로 정보값을 뿌려야한다.  
이 때 **while문**을 사용하게 된다.  

<br>
<pre>
    < ?php 
    while ($array = mysqli_fetch_array($result)){
    ? >

    < table>
        < tr>
            < td><?php echo $array["회원번호"]; ?>< /td>
            < td><?php echo $array["아이디"]; ?>< /td>
            < td><?php echo $array["이름"]; ?>< /td>
            < td><?php echo $array["전화번호"]; ?>< /td>
            < td><?php echo $array["이메일"]; ?>< /td>
            < td><?php echo $array["생일"]; ?>< /td>
            < td><?php echo $array["주소"]; ?>< /td>
            < td>< a href="edit.php?g_idx=<?php echo $array["idx"]; ?>">수정< /a>< /td>
            < td>< a href="#" onclick='del_mem(<?php echo $array["idx"]; ?>)'>삭제< /a>< /td>
        < tr>
    < /table>

    < ?php 
    };
    ? >

</pre>
  
table 태그를 while문 안에 가두면 모든 값이 출력될 때까지 php가 데이터를 가지고 와서 td 태그 안에 뿌리게 된다.   
<br>
<br>

###### 회원정보 수정할 관리자용 edit.php 만들기

<br>
관리자가 별도로 회원정보를 수정할 수 있도록 edit.php를 만든다.  
기존의 edit.php 파일을 가져다가 사용하면 된다.  
   

여기서 수정과 삭제 시에는 관리자가 **'클릭한'** 회원의 정보만 수정되고 삭제되어야 하기 때문에 어떤 회원을 클릭했는지 그 값을 받아와야 한다.  
  
그 값은 GET 방식으로 받아올 수 있다.  
위의 a 링크 태그 안에 url 처럼 전달할 수 있다.

<pre>
    //edit.php로 갈 때 g_idx라는 변수를 만들어서 지금 페이지에서 가지고 있는 idx 값을 보낸다.

    < td>< a href="edit.php?g_idx=<?php echo $array["idx"]; ?>">수정< /a>< /td>
    < td>< a href="#" onclick='del_mem(<?php echo $array["idx"]; ?>)'>삭제< /a>< /td>
</pre>
  
이렇게 url에 넣어 보내는 방식이 **GET** 방식이고 url에 뜬 이 값을 받아 그 페이지에서 사용할 수 있다.
  
<br>

**edit.php**<br>

**1. 관리자 세션 삽입**

우선 이 페이지는 관리자가 사용하는 회원정보 수정 페이지이기 때문에 관리자용 세션을 넣어야 한다.
<br>

<pre>
< ?php
include "../admin_check.php";
? >
</pre>

<br>

**2. 데이터베이스 연결**

사용자 정보를 받아 form 에 뿌려야 하기 때문에 데이터베이스에 연결한다.
<br>

<pre>
< ?php
include "../../inc/dbcon.php";
? >
</pre>

<br>

**3. GET으로 받아온 값을 세션 삼아 데이터를 추출**

데이터베이스에 SELECT문으로 회원정보를 가져와야 하는데,  
get으로 가져온 값이 회원번호이기 때문에 값을 받아다 변수에 담고 where 절의 조건으로 넣어준다.
<br>

<pre>
< ?php
$g_idx = $_GET["g_idx"];

$sql = "select * from members where idx='$g_idx';";
? >
</pre>

<br>

데이터베이스에 쿼리를 전송한 후 array로 데이터를 받는다.
<br>

<pre>
< ?php
$result = mysqli_query($dbcon, $sql);

$array = mysqli_fetch_array($result); 
? >
</pre>


<br>
<br>

###### edit_ok.php 만들기

###### 회원정보 삭제 delete.php 만들기

**delete 함수 만들어 onclick 연결**



###### 회원정보 삭제 delete.php 만들기

**delete 연결 위해 스크립트 만들기**
