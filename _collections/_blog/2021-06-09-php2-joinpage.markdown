---
layout: post
title:  "[PHP] PHP join 페이지 생성하기"
author: Kenna
date:   2021-06-09 17:26:35 +0830
image: https://images.unsplash.com/photo-1611647832580-377268dba7cb?ixid=MnwxMjA3fDB8MHxzZWFyY2h8OHx8cGhwfGVufDB8fDB8fA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60
rating: 15
description: 수업 복습
---

###### PHP
[PHP 공식 홈페이지]("https://www.php.net/")

###### PHP


###### $변수 에 넘어오는 값 담기

<pre>
$u_name = $_POST["u_name"];
$u_id = $_POST["u_id"];
$u_pwd = $_POST["u_pwd"];
$mobile = $_POST["mobile"];
$email = $_POST["email_id"]."@".$_POST["email_dns"];
$birth = $_POST["birth"];
$postalCode = $_POST["postalCode"];
$addr1 = $_POST["addr1"];
$addr2 = $_POST["addr2"];
$agree = $_POST["agree"];
$reg_date = date("Y-m-d");
</pre>

$reg_date에는 date 함수를 사용하고 안에는 날짜형식 작성<br>

$reg_date = date("형식"s);<br>

연도의 Y가 대문자면 네 자리(2000) y 소문자면 (00) 두 자리 연도<br>

시간 표시는 H 시간 : i 분 : s 초  (H 대문자는 24시간 h 소문자는 12시간)<br><br>


###### 데이터베이스 연결하기 DB 접속

mysql 5.x 버전까지는 mysql_connect 사용
mysql 7.x 버전부터는 mysqli_connect 사용<br>


**연결객체**<br>
**mysqli_connect("HOST", "아이디", "비밀번호");**<br>
-> mysql -h localhost -uroot -p 랑 같다.

**DB와 연결**
**mysqli_select_db(연결객체, "DB명");**<br>
-> use front 랑 같다.

mysqli_select_db(연결객체, "DB명")의
연결객체는 위의 mysqli_connect이지만 저 코드를 다 집어 넣으면 너무 복잡하기 때문에<br>

$dbcon = mysqli_connect("HOST", "아이디", "비밀번호");로
변수에 담아 연결객체 파라미터 자리에 넣는다.


**mysqli_select_db($dbcon, "DB명");**<br>
이렇게 쓸 수 있다.

이것도 문장을 두 번 작성해야 하기 때문에 위의 "DB명"을 올려

**$dbcon = mysqli_connect("HOST", "아이디", "비밀번호", "DB명");**<br>
로 만든다.

최종적으로

<pre>
< ?php

$dbcon = mysqli_connect("127.0.0.1", "root", "", "front") or die("DB 접속 실패");

?>

</pre>

로 연결할 수 있다.
<br><br>

###### mysqli charset 설정
위와 같이 mysql DB에 연결하고 테이블에 데이터를 삽입하게 되면 한글이 깨질 수 있다.
이 경우 문자셋 설정이 필요하다.

<pre>

< ?php

$dbcon = mysqli_connect("127.0.0.1", "root", "", "front") or die("DB 접속 실패");
mysqli_set_charset($dbcon, "utf8");

?>


</pre>

아래에 charset 선언부를 붙여준다.

<br><br>

###### 데이터베이스에 전달할 쿼리 생성

PHP에서는 큰 따옴표 안에 변수를 넣는다.<br>

**$variable = "value";**

각 변수를 구분하는 ,는 문자다.<br>


따라서 아래와 같이 쉼표와 변수를 구분한다.

**'".$name."'**
<br>

"따옴표와 변수를 **.** 연산자로 이어준다.
insert 문을 아래와 같이 생성할 수 있다.

<pre>

< ?php

insert into members (
u_name, u_id, u_pw, mobile, email, birth, postalCode, addr1, addr2, reg_date)
values('".$u_name."','".$u_id."','".$u_pwd."','".$mobile."','".$email."', '".$birth."','".$postalCode."','".$addr1."','".$addr2."','".$reg_date."'
);

?>

</pre>

만약 데이터를 화면에 출력해야 한다면 아래와 같이 사용한다.

<pre>

< ?php

echo "insert into members (
u_name, u_id, u_pw, mobile, email, birth, postalCode, addr1, addr2, reg_date)
values('".$u_name."','".$u_id."','".$u_pwd."','".$mobile."','".$email."', '".$birth."','".$postalCode."','".$addr1."','".$addr2."','".$reg_date."'
);";

?>

</pre>

하지만 전체를 쌍따옴표로 감싼다면 작은따옴표만을 이용해 변수와 쉼표를 구별할 수 있다.

<pre>

< ?php

echo "insert into members (u_name, u_id, u_pw, mobile, email, birth, postalCode, addr1, addr2, reg_date) values ('$u_name','$u_id','$u_pwd','$mobile','$email','$birth','$postalCode','$addr1','$addr2','$reg_date');";

?>

</pre>

이 경우엔 개행도 가능하다.

<pre>

< ?php

echo "insert into members (
    u_name, u_id, u_pw, mobile, email, birth, postalCode, addr1, addr2, reg_date
    ) values (
        '$u_name','$u_id','$u_pwd','$mobile','$email','$birth','$postalCode','$addr1','$addr2','$reg_date');"; 

?>

</pre>

위의 긴 코드를 실행시키기 위해서는 다시 변수에 담아 사용하는 것이 편하다.

<pre>

< ?php

$sql = "insert into members (
    u_name, u_id, u_pwd, mobile, email, birth, postalCode, addr1, addr2, reg_date
    ) values (
        '$u_name','$u_id','$u_pwd','$mobile','$email','$birth','$postalCode','$addr1','$addr2','$reg_date');";
?>

</pre>

위의 코드를 echo $sql; 로 실행시켜도 echo "insert into ..." 와 결과는 같다.
<br>
<br>



###### 데이터베이스에 값 전달하기

값을 전달하는 쿼리는<br>
**mysqli_query("연결객체", "전달할 쿼리);**로 쓴다.

여기서의 연결객체는 위의
**mysqli_connect**쿼리이고 전달할 쿼리는
위의 **insert into** 문이다.

두 개 다 변수에 미리 담아두었기 때문에 바로 변수로 사용할 수 있다.

<pre>

< ?php

mysqli_query($dbcon, $sql);

?>

</pre>

변수에 안 담아두면 이렇게 된다.


<pre>

< ?php

mysqli_query(mysqli_connect("127.0.0.1", "root", "", "front") or die("DB 접속 실패");, "insert into members (u_name, u_id, u_pwd, mobile, email, birth, postalCode, addr1, addr2, reg_date) values ('$u_name','$u_id','$u_pwd','$mobile','$email','$birth','$postalCode','$addr1','$addr2','$reg_date');";);

?>

</pre>

<br><br>
![...](https://i.imgflip.com/1d1kyo.jpg))<br><br><br>

###### 데이터베이스 연결 종료

데이터베이스를 연결해서 할 작업이 모두 종료되면 데이터베이스와의 연결을 끊는 것이 보안상 안전하다.

연결 종료 쿼리는
**mysqli_close($dbcon);** <br>

()에 안 넣으면 
https://stackoverflow.com/questions/24027546/warning-mysqli-close-expects-parameter-1-to-be-mysqli
와 같은 오류가 생길 수 있다.
<br>

###### result.php 만들어서 결과 보여주기

데이터가 이동한 부분은 사용자에게 보여지지 않고 결과페이지가 전송되어야 한다.
이렇게 페이지를 바꿔주는 것을 리디렉션redirection 이라고 한다.
m.naver.com 처럼 주소를 바꿔준다.
이 기능은 php언어로 구현하는 것이 아니라 script 언어로 구현한다.

<pre>
< ?php

echo "

    < script script type=\"text/javascript\">
    location.href=\"result.php\";

    </ script> 
    
";

?>
</pre>

이 스크립트 코드를 echo에 넣어 화면에 출력하거나 
아예 <?php ?> 코드 바깥에 넣어주면 실행된다.

location.href 외에도<br>
<pre>
    location.replace;
    location.reload;
</pre>
를 사용할 수 있다.<br>

뒤로가기 같은 페이지 이동은 (← , →) <br>
<pre>
history.back();
history.forword();
history.go(); <- 양수, 음수로 조절한다.

</pre>