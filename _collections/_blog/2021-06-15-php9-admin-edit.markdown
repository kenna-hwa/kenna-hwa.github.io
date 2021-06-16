---
layout: post
title:  "[PHP] 관리자권한으로 회원정보 수정,삭제 연결하기"
author: Kenna
date:   2021-06-16  10:26:35 +0830
image: https://images.unsplash.com/photo-1611647832580-377268dba7cb?ixid=MnwxMjA3fDB8MHxzZWFyY2h8OHx8cGhwfGVufDB8fDB8fA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60
rating: 26
description: 수업 복습
categories : PHP
tags: PHP
---

###### PHP
[PHP 공식 홈페이지]("https://www.php.net/")


###### 회원정보 수정할 관리자용 edit.php 만들기

<br>
관리자가 별도로 회원정보를 수정할 수 있도록 edit.php를 만든다.  
기존의 edit.php 파일을 가져다가 사용하면 된다.  
필요하다면 회원에게는 수정하지 못하게 해둔 이름과 아이디도 수정할 수 있도록 input을 넣고 수정 데이터를 보낼 수 있다.  


여기서 수정과 삭제 시에는 관리자가 **'클릭한'** 회원의 정보만 수정되고 삭제되어야 하기 때문에 어떤 회원을 클릭했는지 그 값을 받아와야 한다.  
  
그 값은 GET 방식으로 받아올 수 있다.  
위의 a 링크 태그 안에 url 처럼 전달할 수 있다.

<pre>
    //edit.php로 갈 때 g_idx라는 변수를 만들어서 지금 페이지에서 가지고 있는 idx 값을 보낸다.

    < td>< a href="edit.php?g_idx=< ?php echo $array["idx"]; ? >">수정< /a>< /td>
    < td>< a href="#" onclick='del_mem(< ?php echo $array["idx"]; ? >)'>삭제< /a>< /td>
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

만든 edit_ok.php 에는 GET방식으로 회원번호를 받아와 회원번호를 조건으로 데이터를 뿌려주고 있다.

  
**1. 관리자 세션 삽입**

관리자만 이용할 수 있도록 관리자용 세션을 추가한다.
<br>

<pre>
< ?php
include "../admin_check.php";
? >
</pre>

<br>

**2. POST방식으로 값 받기**
  
edit.php 페이지에서 POST 방식으로 보낸 값을 변수에 담아 받는다.
<br>

<pre>
< ?php

$g_idx = $_POST["idx"];
$u_pwd = $_POST["u_pwd"];
$mobile = $_POST["mobile"];
$email = $_POST["email_id"]."@".$_POST["email_dns"];
$birth = $_POST["birth"];
$postalCode = $_POST["postalCode"];
$addr1 = $_POST["addr1"];
$addr2 = $_POST["addr2"];

? >
</pre>

<br>

**3. 데이터베이스 연결**

수정한 사용자의 정보를 데이터베이스로 보내야 하기 떄문에 데이터베이스를 연결한다.
<br>

<pre>
< ?php
include "../../inc/dbcon.php";
? >
</pre>

<br>

**4. 회원정보 수정을 위한 쿼리 작성**


연결한 데이터베이스에 수정 정보를 보내는 쿼리를 작성한다.  
이때 **UPDATE문**을 사용한다.   
비밀번호를 입력해 수정할 때와 비밀번호를 입력하지 않고 수정할 때 두 가지의 조건이 있기 때문에  
조건문에 담아 쿼리를 작성한다.
<br>

<pre>
< ?php

if($u_pwd){

//비밀번호를 입력한 경우
$sql = "update members set u_pwd = '$u_pwd', mobile = '$mobile', email = '$email', birth = '$birth', postalcode = '$postalCode', addr1 = '$addr1', addr2 = '$addr2' where idx = $g_idx;";
}else{
//비밀번호를 입력하지 않은 경우
$sql = "update members set mobile = '$mobile', email = '$email', birth = '$birth', postalcode = '$postalCode', addr1 = '$addr1', addr2 = '$addr2' where idx = $g_idx;";

};

? >
</pre>

<br>

**5. 쿼리 전송**

작성한 쿼리를 데이터베이스로 보내 정보를 업데이트한다.
<br>

<pre>
< ?php
mysqli_query($dbcon, $sql);
? >
</pre>

<br>

**6. 페이지 이동**

수정을 완료하고 데이터베이스를 종료한 다음 내용을 확인하기 위해 다시 페이지를 list.php로 이동시킨다.
<br>

<pre>
< ?php



//** DB 종료
mysqli_close($dbcon);



echo "

    < script type=\"text/javascript\">
    alert(\"정보가 수정되었습니다.\");
    location.href=\"list.php\";

    < /script> 
    
";
? >
</pre>

<br><br>

###### delete.php 만들기

기존의 회원 탈퇴와 방식은 같다.  
그러나 관리자가 이용하는 회원 삭제 페이지이기 떄문에 관리자 세션을 추가하고  
list에서 링크로 보낸 값을 받기 위해 GET 방식으로 받은 변수로 회원을 구분한다.  
<br>

링크를 클릭하자마자 바로 삭제되는 것은 후회가 남을 수 있으므로 후회가 남지 않도록 삭제 링크에는  
**function()**으로 이동해 **confirm**메시지가 뜬 다음 delete.php로 이동할 수 있도록 절차를 만든다.
<br>
<br>

**1. onclick에 연결할 함수 만들기**

스크립트에 function del_mem() 이라는 함수를 만든다.  
confirm 메세지가 뜨고 나서 페이지를 이동하도록 한다.

<pre>
< script type="text/javascript">
    function del_mem(idx) {
        var ck = confirm("정말 삭제하시겠습니까? 삭제한 아이디는 다시 복구할 수 없습니다.");
        if(ck == true){
            location.href="delete.php?g_idx="+idx;
        };
    };
< /script>
</pre>
<br>

**2. 삭제 링크에 onclick으로 함수 담기**
<br>
<pre>
< td>< a href="#" onclick='del_mem(< ?php echo $array["idx"]; ? >)'>삭제< /a>< /td>
//del_mem()의 파라미터 부분에 array로 받아온 회원번호를 넣어 링크의 뒷부분에 연결되도록 한다.
</pre>
<br>


**3. delete.php에 관리자 세션 삽입**

해당 페이지를 관리자만 이용할 수 있도록 관리자용 세션을 추가한다.
<br>


<pre>
< ?php
include "../admin_check.php";
? >
</pre>

<br>

**4. 데이터베이스에 연결**

사용자 정보를 데이터베이스에서 삭제해야하므로 데이터베이스에 연결한다.
<br>

<pre>
< ?php
include "../../inc/dbcon.php";
? >
</pre>

<br>


**5. GET방식으로 받은 값 변수에 담기**

edit_ok.php 처럼 GET 방식으로 받은 값을 변수에 담아 삭제할 회원인지 구분한다.
<br>

<pre>
< ?php
$g_idx = $_GET["g_idx"];
? >
</pre>

<br>

**6. 삭제할 회원을 조건에 담아 쿼리 작성해 데이터베이스로 전송**

DELETE문 혹은 UPDATE문으로 쿼리를 작성해 데이터베이스로 보낸다.
<br>

<pre>
< ?php

//DELETE문 사용

$sql = "delete from members where idx=$g_idx;";


//UPDATE문 사용

$sql = "update members set u_pwd='', mobile='', email='', birth=null, postalcode='', addr1='', addr2='' where idx=$g_idx;";


//쿼리 전송

mysqli_query($dbcon, $sql);

? >
</pre>

<br>

**7. 삭제완료 메시지 띄우고 회원정보 페이지로 이동**

삭제 완료 후 메세지 출력하고 회원정보 페이지로 이동하는 스크립트를 삽입한다.
<br>

<pre>
< ?php
echo "
    < script type=\"text/javascript\">
    alert(\"회원정보 삭제 처리되었습니다.\");
    location.href=\"../members/list.php\";
    < /script> 
";
? >
</pre>

<br>

