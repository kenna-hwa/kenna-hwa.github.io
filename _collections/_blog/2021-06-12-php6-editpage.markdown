---
layout: post
title:  "[PHP] 회원정보 수정 페이지 만들기"
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
다만 일반적으로 수정이 가능한 정보와 불가능한 정보가 있기 때문에,  
수정이 불가능한 정보는 데이터를 받아와서 출력만 해주고 수정이 가능한 정보는 **'update'** 쿼리를 이용해 덮어쓰기 해준다.  

<br>

**회원정보 수정 페이지 만들기**
<br>

회원가입 페이지를 그대로 가져와서 **수정하지 않을 부분**인 이름, 아이디, 약관동의 부분은 input 태그를 뺀다.  
이름, 아이디에는 기존 입력한 정보를 출력할 수 있도록 echo로 기존 정보를 받아온다.  
비밀번호는 기존 정보를 노출하면 보안상 문제가 될 수 있으므로 join.php와 동일하게 둔다.  
나머지 정보들은 기존 정보를 input 에 그대로 출력해야하므로 input 태그에 value 속성 값으로 **< ?php echo $가져올컬럼의변수 ?>**를 넣는다.

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

아래 코드는 혹시 세션이 없이 진입했는지 아닌지 확인하면서, 세션값이 없으면 오류 메세지를 출력하지 말라는 삼항연산자다.
<br><br>
<br><br>

**데이터베이스에서 기존 정보 받아오기**
<br>

데이터베이스에서 기존 정보를 받아오려면 우선 데이터베이스에 연결되어 있어야 한다.

외부파일 **include**를 한다.

<pre>
< ?php

include "../inc/dbcon.php";

? >
</pre>
<br>

**데이터베이스에  보낼 쿼리를 작성**
<br>

우선 작성할 것은 페이지에 노출해야 할 기존 정보들을 부르는 select문을 작성한다.

<pre>
< ?php 

$sql = "select * from members where idx='$s_idx';";

? >
</pre>

위 쿼리는 가입된 회원 정보가 들어있는 members 테이블에 세션값인 s_idx 번호의 정보값을 전부 가져오는 문장이다.  
<br>
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

? >
</pre>
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

? >
</pre>
<br>
<br>

**버튼 생성**
<br>

정보 수정 페이지에서 필요한 돌아가기, 정보수정, 회원탈퇴 세 개의 버튼을 만든다.  

**돌아가기** 버튼은 button 타입은 button으로 onclick 이벤트 리스너에 location="index파일 경로" 혹은 이동하고 싶은 경로를 설정한다.  
뒤로 가고 싶으면 history.go(-1) 함수를 설정해 한 페이지 뒤로가기를 설정할 수도 있다.

별도로 js파일에 함수를 만들어서 onclick으로 넣을 수도 있다.

<br>

**정보수정** 버튼은 button 타입은 submit으로 하고 form 태그에 onsubmit 이벤트 리스너로 스트립트를 걸어둔다.  
스크립트가 필요한 이유는 필수 입력해야 하는 부분이 입력값을 넣지 않은 부분이 있는지, 조건에 맞지 않는 값을 넣지는 않았는지 검증하기 위해서다.  
회원 가입 시 제시한 조건과 동일한 유효성 검사 코드를 이용해서 검사를 진행하고,  
action 값으로 설정된 edit_ok.php 파일을 통해 데이터베이스에 전달할 수 있도록 한다.  

<br>

**회원탈퇴** 버튼은 회원 탈퇴를 하기 위한 페이지를 만들어서 클릭 시 해당 페이지로 진입할 수 있도록 한다.  
onclick 이벤트 리스너에 페이지로 이동하는 js함수를 연결시킨다.
<br><br>

###### edit_ok.php 페이지 만들기

edit.php 페이지에서 form 태그로 넘어온 edit_ok.php는 단순 데이터 전송 작업만 하기 때문에 별도로 HTML 마크업을 하지 않는다.  
  
가장 처음 해야할 일은 세션을 가져오고, 이전 페이지에서 넘어온 값을 변수에 담아 쿼리를 작성해 데이터베이스에 넘기는 일이다. 
<br><br>
  
**세션 스타트 함수**
<br>
<pre>
< ?php

session_start();
$s_idx = isset($_SESSION[" s_idx"])? $_SESSION[" s_idx"] : ""; 

? >
</pre>

해당 함수를 넣어 세션을 가지고 들어온다.  
  
<Br>
<br>

**이전 페이지에서 값 가져오기**
<br>
회원정보 수정 페이지에서 post 방식으로 넘어온 각 input의 값들을 변수에 담아 받는다. 

<pre>
< ?php

$u_pwd = $_POST["u_pwd"];
$mobile = $_POST["mobile"];
$email = $_POST["email_id"]."@".$_POST["email_dns"];
$birth = $_POST["birth"];
$postalCode = $_POST["postalCode"];
$addr1 = $_POST["addr1"];
$addr2 = $_POST["addr2"];

? >
</pre>
<Br>

위와 같이 수정이 가능한 부분만 input 태그를 열어 수정 내용을 받아준다.

여기에서 특이한 점은 pwd외에 정보들은 value 값을 통해 데이터베이스의 존재하던 정보를 미리 노출했는데 이로서 정보가 수정되었는지에 상관없이 모든 정보를 한 번에 update 할 수 있다.  
만약 필수로 입력해야 하는 정보들이 있다면 스크립트를 통해 유효성 검사를 한 다음에 submit으로 넘길 수 있도록 하는 것이 좋다. 
<br><br>
(나는 처음에 기존 데이터베이스 정보를 다시 다 받아서 if 문으로 서로 다른지 != 비교해서 다를 경우에 update문이 실행되도록 했는데,  
이것보다 스크립트로 먼저 필수 입력 부분을 제대로 입력했는지 검수한 다음, 기존 정보도 그대로 update를 하면 된다는 것을 배웠다.)
<br><br>

**데이터베이스 연결**
<br>
데이터베이스에 수정한 정보를 전달해야하므로 include 명령어로 데이터베이스에 연결한다.  

<pre>
< ?php

include "../inc/dbcon.php";

? >
</pre>
<br><br>

**쿼리 작성**
<br>

이번 쿼리는 update를 사용한다. 
여기서 주의할 점은 **'비밀번호**는 출력되지 않은 비밀번호를 입력하지 않아도 다른 정보를 수정해 제출할 수 있는데,  
**비밀번호가 비어있는 경우** 반드시 비밀번호를 제외한 나머지가 update가 되도록 하고,   
**비밀번호를 입력한 경우** 비밀번호를 포함해서 전부 update하도록 해야 한다.  
<br>
비밀번호가 없는데 모든 정보값을 업데이트하게 되는 경우 해당 회원이 비밀번호는 null 값이 되어버린다.

<br><br>

**조건 처리**
<br> 
  
비밀번호를 입력한 경우 - 패스워드 포함  
<pre>
< ?php

$sql = "update members set u_pwd = '$u_pwd', mobile = '$mobile', email = '$email', birth = '$birth', postalcode = '$postalCode', addr1 = '$addr1', addr2 = 'addr2' where idx = $s_idx;";
}else{

    ?>
</pre>

비밀번호를 입력하지 않은 경우 - 패스워드 제외   

<pre>
< ?php

$sql = "update members set mobile = '$mobile', email = '$email', birth = '$birth', postalcode = '$postalCode', addr1 = '$addr1', addr2 = 'addr2' where idx = $s_idx;";

};

? >
</pre>
<br><br>

**쿼리 전송**
<br>

쿼리를 데이터베이스에 전송해 정보를 업데이트 한다.  

<pre>
< ?php

mysqli_query($dbcon, $sql);

? >
</pre>
<br>
쿼리가 select 문일때는 결과를 가지고 와야 해서 (fetch 써야 해서) 변수에 담는게 좋고 아니면 그냥 써도 된다.  
헷갈리면 일단 변수에 담아도 된다.  
  
<br><br>

**페이지 이동**
<br>

<pre>
< ?php

echo "

    < script type=\"text/javascript\">
    alert(\"정보가 수정되었습니다.\");
    location.href=\"edit.php\";

    </ script> 
    
";

? >
</pre>
<br>

정보보기 페이지가 필요하다면  
edit 페이지에서 input 태그 다 빼고 값만 받아오면 된다.  

<br><br>

**DB 종료** <br>  

<pre>
< ?php

mysqli_close($dbcon);

? >
</pre>