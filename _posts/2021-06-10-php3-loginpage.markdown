---
layout: post
title:  "[PHP] PHP 로그인페이지 만들기"
author: Kenna
date:   2021-06-10 17:26:35 +0830
image: https://images.unsplash.com/photo-1611647832580-377268dba7cb?ixid=MnwxMjA3fDB8MHxzZWFyY2h8OHx8cGhwfGVufDB8fDB8fA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60
rating: 16
description: 수업 복습
categories : [PHP]
tags: [PHP]
---

###### PHP
[PHP 공식 홈페이지]("https://www.php.net/")

###### PHP


###### 로그인페이지 만들어서 로그인 진행하기


login.php 파일에 html로 페이지 구성

form action 값을 login_ok.php로 설정

<br><br>

###### login_ok.php 만들기

**이전 페이지에서 데이터 가져오기**<br>

변수명 = $_메소드방식["필드의 name 속성값"];

<pre>
< ? php

$u_id = $_POST["u_id"]; //post 메소드로 전달받은 u_id(로그인 아이디)값을 변수에 넣는다.
$u_pwd = $_POST["u_pwd"];//post 메소드로 전달받은 u_pwd(로그인 패스워드)값을 변수에 넣는다.

? >
</pre>

넘어오는 데이터 확인하기

<pre>
< ? php

echo "아이디:".$u_id."/"."비밀번호 :".$u_pwd;

? >
</pre>
<br><br>

###### 매번 써야하는 DB연결 include 하기


**DB 연결**<br>

<pre>
< ? php

$dbcon = mysqli_connect("localhost", "root", "", "front") or die("DB 접속 실패");
mysqli_set_charset($dbcon, "utf8");

? >
</pre>

위의 코드를 매번 삽입하는 것보다 외부 파일로 만들어서 삽입하는 것이 관리가 쉽다.(추후 호스트가 바뀌거나 할 때도 편하다. 외부 파일의 장점)

외부 파일은

<pre>

< script src=""></ script> - javascript
import "aa.src" - css
obj.load("파일명.확장자")-jQuery

</pre>

이것들 처럼 PHP 에서는 **import** 로 삽입한다.


파일을 불러올 위치에 <br>

**include "../inc/dbcon.php";**<br>

여러가지 방법이 있는데,
include_once는 해당 파일을 한 번 만 불러와도 될 때 사용하고
require은 좀 더 엄격한 방식이다.
[참고할 네이버 블로그]("https://m.blog.naver.com/bgpoilkj/221274098558"
)

<br><br>

###### 데이터베이스에서 id값과 pwd값 불러오기<br>

SELECT문은 INSERT UPDATE DELETE와 다르게 결괏값을 보여준다.
그래서 SELECT문으로 데이터베이스에 있는 id 값과 pwd 값을 확인해서 사용자가 입력한 id,pwd값과 비교할 수 있다.

<pre>

< ? php

$sql = "SELECT idx, u_name, u_id, u_pwd FROM members WHERE u_id='$u_id';";

? >

</pre>

echo $sql; 로 값을 확인해볼 수 있다.
위의 쿼리가 실행되면 사용자가 id값을 맞게 넣어준 것


**DB에 쿼리 전달하기**

DB에 쿼리를 날리는 것은 항상 DB연결이 선행되어야 하므로 코드도 순서대로 짜야한다.

<pre>
< ? php

//쿼리 보내는 함수
mysqli_query($dbcon, $sql);

? >
</pre>
위의 함수를 변수에 넣어 사용한다.

<pre>
< ? php

$result = mysqli_query($dbcon, $sql)

? >
</pre>

<br><br>

**결괏값 가져오기**

DB에 SELECT 문으로 쿼리를 날리면 결괏값을 가져오는 문장을 사용해야 한다.

<pre>
< ? php

mysqli_fetch_row()
mysqli_fetch_array()
mysqli_num_rows()

? >
</pre>

**mysqli_fetch_row(mysqli_query()) :**<br>
날린 쿼리의 결괏값을 **'필드 순서'**에 따라 가져온다. 결괏값 중 첫번째 행만 출력된다.
<br>

mysqli_fetch_row($result);
하면 $result 쿼리를 데이터베이스에 날려서 받은 결괏값의 첫번째 행만 출력한다. 게시판과 같이 여러 개의 결괏값을 보여줘야 하는 경우는 반복문 안에 담아서 출력해야한다.

$row = mysqli_fetch_row($result);
결괏값을 화면에 출력하려면 $row[2]."/".$row[3] 한다. (현재 $result에서 받아오는 값은 총 4개지만 필요한 id와 pwd는 인덱스 2과 3을 사용한다.)
<br>

**mysqli_fetch_array(mysqli_query()) :**<br>
날린 쿼리의 결괏값을 **'필드 이름'**에 따라 가져온다. 결괏값 중 첫번째 행만 출력된다.
<br>

mysqli_fetch_array($result);를 변수에 담으면,
$array = mysqli_fetch_array($result);
echo $array["u_id"]."/".$array["u_pwd"];

**mysqli_num_rows(mysqli_query()) :**<br>
날린 쿼리의 결괏값의 **'행의 갯수'**를 가져온다. 결괏값이 숫자로 표시된다.
있는지 없는지 확인할 때 유용하다.
SELECT count(*) FROM members WHERE u_id='admin';
과 똑같은 말이다.

이것도 변수에 넣어 사용하는 것이 편하다.
$num = mysqli_num_rows(mysqli_query($result));
echo $num;

<br>
따라서 num_rows로 아이디가 있는지 확인한 후 패스워드 일치를 확인하기 위해서,
fetch_row나 fetch_array 둘 중 하나는 있어야 한다.
어차피 입력된 id 값이 데이터에 있어야 비밀번호를 비교할 수 있기 때문에 둘 중 아무거나 사용해도 된다.

<br><br>

###### 조건 처리하기

로그인 기능 구현 시 처리해야 하는 조건은 두 가지이다.

1. 조건에 맞는 아이디가 없을 때 - 즉 회원이 아닐 때.
2. 조건에 맞는 아이디가 있을 때 - 즉 회원일 때.

1번의 경우 조건에 맞는 아이디가 없기 때문에 "아이디를 다시 입력해주세요." 라는 안내 문구가 노출되면 되고 2번은 조건에 맞는 아이디가 있는 회원이 접속을 시도하는 것이기 때문에 비밀번호를 검증해 로그인 시켜주면 된다.

1. 조건에 맞는 아이디가 없을 때


만약에 num_rows로 받아온 값이 없으면! - 회원이 아니니까 메세지 출력

if       ( !$num )        {

       echo "
        < script type=\"text/javascript\">
        alert(\"일치하는 아이디가 없습니다.\");
        history.back();
        < /script>
        ";
    exit;


아니면 (num_rows로 받아온 값이 있으면) - 회원이니까 비밀번호 검증
else 문 안에 if문을 중첩한다.

} else {

$array = mysqli_fetch_array($result);

array로 select로 가져온 값들을 변수에 담아 if문으로 비교한다.

$g_idx = $array["idx"];
$g_name = $array["u_name"];
$g_id = $array["u_id"];
$g_pwd = $array["u_pwd"];
echo $g_idx."/".$g_name."/".$g_id."/".$g_pwd;



if  ( $u_pwd != $array["u_pwd"]  )  {
    echo "
    < script type=\"text/javascript\">
        alert(\"비밀번호가 일치하지 않습니다.\");
        history.back();
        < /script>
        ";
        exit; 

};

<br><br>

###### 로그인 완료 후 Session 만들어서 유지하기

지금까지 사용한 데이터들은 다른 페이지에서 사용할 수 없다.
회원 정보를 다시 조회해서 매 페이지마다 로그인 과정을 거칠 수 없기 때문에
하나의 홈페이지의 모든 페이지에서 이 값을 공유해야 한다.<br>


**Session**<br>

모든 페이지가 공통으로 사용하는 변수<br>


**Session 생성**<Br>

<pre>
< ? php

$_SESSION["세션변수명"] = 저장할 값;
"세션변수명'은 직접 지어준다.


$_SESSION["s_idx"] = $array["idx"];
$_SESSION["s_name"] = $array["u_name"];
$_SESSION["s_id"] = $array["u_id"];

? >
</pre>
<br>

###### Session을 사용하겠다고 알려주기

문서 맨 위에 session_start();

세션을 사용하려고 하는 문서에는 전부 상단에 <br>session_start();를 사용해야한다.

<br>

###### 페이지 이동시키기

<pre>

< ? php

echo "

    < script type=\"text/javascript\">
    location.href=\"../index.php\";

    </ script> 
    
";
? >

</pre>
