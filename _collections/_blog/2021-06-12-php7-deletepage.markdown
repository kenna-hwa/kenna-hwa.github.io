---
layout: post
title:  "[PHP] 회원탈퇴하기 페이지 만들기"
author: Kenna
date:   2021-06-12 15:26:35 +0830
image: https://images.unsplash.com/photo-1611647832580-377268dba7cb?ixid=MnwxMjA3fDB8MHxzZWFyY2h8OHx8cGhwfGVufDB8fDB8fA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60
rating: 20
description: 수업 복습
categories : PHP
tags: PHP
---

###### PHP
[PHP 공식 홈페이지]("https://www.php.net/")


###### 회원탈퇴 delete.php 페이지 만들기

edit.php에서 연결한 회원탈퇴 버튼으로 연결되도록 한 delete.php를 만든다.  
버튼에 연결한 스크립트에는 반드시
탈퇴하시겠습니까? 네/아니오 alert를 띄워야 실수로 사용자가 정보를 삭제하는 일이 일어나지 않는다.  
특히 재가입 시 동일한 아이디는 사용할 수 없음을 알려야 데이터베이스 관리가 쉽다.  
<br>

**데이터베이스 구성**
  
회원탈퇴의 경우 두 가지의 방법이 있다.

<br><br>
  
**테이블을 하나만 사용하는 경우**  

<br>
회원정보members 테이블에서 idx와 아이디를 제외한 나머지 정보를 삭제하는 쿼리를 만들고  
아이디는 unique를 주거나 회원가입 form에서 에서 id가 기존 데이터베이스에 있는지 검증하는 과정을 만들어  
가입을 진행하게 하면 회원 탈퇴 시 중복된 아이디를 사용하지 못하도록 할 수 있다.  
  
이 경우 로그인 할 때 띄우는 메세지가  
'아이디를 찾을 수 없습니다.'  
'비밀번호가 틀렸습니다.'  
가 아닌  

**'아이디와 비밀번호를 확인해주세요.'**와 같은 통합된 메시지를 전달해야 탈퇴한 회원이 사용한 아이디임을 들키지 않을 수 있다.
<br><br>

**테이블 두 개를 사용하는 경우**
  
<br>
회원정보 members 테이블에서는 모든 정보를 삭제하고  
별도로 탈퇴한 회원의 아이디와 이름 정도를 저장하는 테이블을 만들어  
정보 삭제 쿼리와 정보 저장 쿼리를 날려 삭제와 저장을 동시에 진행한다.  
이 경우에는 members 테이블에 빈 값이 줄어들고 데이터를 관리하기 용이해지지만    
회원 가입 페이지에서 탈퇴한 회원의 아이디를 걸러낼 수 있어야 하기 때문에    
가입 페이지에서 탈퇴한 회원 테이블의 정보를 받아오고 검증하는 과정이 필요하다.  

수업에서는 첫 번째 방식을 적용했다.  
<br>
  
**세션을 먼저 연결**
<br>
<br>
회원 탈퇴는 회원만 할 수 있기 때문에 회원 검증을 위해 세션을 받아온다.  

<pre>

< ?php

session_start();
$s_idx = isset($_SESSION["s_idx"])? $_SESSION["s_idx"] : ""; 

?>

</pre>
<br>
  
**데이터베이스에 연결**
<br>
<br>
데이터베이스에 있는 회원의 정보를 삭제해야 하기 때문에 include로 데이터베이스에 연결한다.

<pre>

< ?php

include "../inc/dbcon.php";

?>

</pre>
<br>

**데이터베이스에 날릴 삭제 쿼리 작성**
<br>
<br>
회원 정보를 삭제할 쿼리를 작성한다.  
이 때 아이디는 제외해야 추후 중복된 아이디로 가입하는 것을 방지할 수 있다.   
  
여기서는 회원번호, 아이디, 가입일자를 제외하고 update로 null 값을 만드는 쿼리를 넘긴다.  
  
<pre>

< ?php

$sql = "update members set u_pwd='', mobile='', email='', birth=Null, postalcode='', addr1='', addr2='' where idx=$s_idx;";

?>

</pre>
<br>
  

간단하게는 delete문으로 그냥 다 삭제하는 방법이 있다.
  
<pre>

< ?php

$sql = "delete from members where idx=$s_idx;";

?>

</pre>
<br>
  
  
**쿼리 전달**
<br>
<br>
위에서 작성한 쿼리를 데이터베이스에 전달해줘야 한다.  
<pre>
< ?php

mysqli_query($dbcon, $sql);

?>
</pre>
<br>


**세션 삭제**
<br>
<br>
회원 탈퇴를 하고 나면 당연히 세션이 삭제되어야 사용자가 탈퇴하고 세션이 유지되지 않는다.  
로그아웃과 같다.  

<pre>
< ?php

unset($_SESSION["s_idx"]);
unset($_SESSION["s_name"]);
unset($_SESSION["s_id"]);

?>
</pre>
<br>

**페이지 이동**
<br>
<br>
페이지를 이동시켜 종료된 세션을 이어나간다.
<pre>
< ?php

echo "
    < script type=\"text/javascript\">
    alert(\"처리되었습니다.\");
    location.href=\"../index.php\";
    </ script> 
";

?>
</pre>
<br>