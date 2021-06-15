---
layout: post
title:  "[jQuery] Ajax로 중복 아이디 검색하기"
author: Kenna
date:   2021-06-15 17:26:35 +0830
image: https://images.unsplash.com/photo-1611647832580-377268dba7cb?ixid=MnwxMjA3fDB8MHxzZWFyY2h8OHx8cGhwfGVufDB8fDB8fA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60
rating: 23
description: 수업 복습
categories : jQuery
tags: jQuery
---

###### jQuery
[jQuery 공식 홈페이지]("https://jquery.com/")  
[비동기 스크립트 Ajax 공부하기 MDN]("https://developer.mozilla.org/ko/docs/Web/Guide/AJAX/Getting_Started")  
[블로그 post 확인하기]("https://kenna-hwa.github.io/blog/2021-05-20-javascript-dom-ajax.html")  


###### 아이디 ajax 방식으로 검색하기

아이디 중복확인을 팝업으로 처리하지 않고  
그 페이지에서 바로 확인하고 사용할 수 있도록  
페이지로 넘기지 않고 그 페이지에서 바로 데이터를 받아와서 상태변화를 시키는 것을  
**Ajax 방식**이라고 한다.  

<br>
<br>

###### jQuery 가져오기
CDN 방식으로 jQuery를 가져온다.  

<pre>
< script src="https://code.jquery.com/jquery-3.6.0.js">
< /script>
</pre>
<br>
<br>

###### jQuery 코드 작성

jQuery는 항상 아래와 같이 시작한다.  
<br>
<pre>
$ (document).ready(function(){

사용할 스크립트

});
</pre>
<br>
<br>

###### 아이디 중복확인 버튼에 함수를 추가하고 아이디 값을 변수로 가져오기

<br>
<pre>
$ (document).ready(function(){

$ (".btn_idCheck").click(function(){ //아이디 중복확인 버튼을 클래스 방식으로 가져옴

var u_id = $(".u_id").val(); //아이디 값을 변수로 가져오기


    });

});
</pre>
<br>
<br>

###### 변수로 가져온 아이디 값의 유효성 검증하기

<br>
<pre>
$ (document).ready(function(){

$ (".btn_idCheck").click(function(){ //아이디 중복확인 버튼을 클래스 방식으로 가져옴

var u_id = $(".u_id").val(); //아이디 값을 변수로 가져오기

        if (!u_id) { //아이디를 입력하지 않았을 때
            $ (".id_txt").html("아이디를 입력하세요");
            $ (".u_id").focus();
            return false;
        } else if (u_id.length < 4 || u_id.length > 12) { //입력된 아이디가 숫자에 맞지 않았을 떄
            $ (".id_txt").html("아이디는 4~12글자만 입력할 수 있습니다.");
            $ (".u_id").focus();
            return false;
        };
    });

});
</pre>
<br>
<br>


###### 유효성 검사를 다 통과하고 나면 데이터베이스에서 아이디가 있는지 없는지 찾는다.

<br>
<pre>
$ (document).ready(function(){

$ (".btn_idCheck").click(function(){ //아이디 중복확인 버튼을 클래스 방식으로 가져옴

var u_id = $(".u_id").val(); //아이디 값을 변수로 가져오기

        if (!u_id) { //아이디를 입력하지 않았을 때
            $ (".id_txt").html("아이디를 입력하세요");
            $ (".u_id").focus();
            return false;
        } else if (u_id.length < 4 || u_id.length > 12) { //입력된 아이디가 숫자에 맞지 않았을 떄
            $ (".id_txt").html("아이디는 4~12글자만 입력할 수 있습니다.");
            $ (".u_id").focus();
            return false;
        } else { //위의 두 규칙에 맞는다면
            //그 아이디 있어 없어?

            $.ajax({

                //데이터 처리 페이지 연결

                url:"search_id_resultcopy.php",

                //데이터 처리 방식 
                
                type:"post",

                //어떤 데이터를 보낼 지 {변수 : 값} 형식으로 작성
                //{변수:값, 변수:값, 변수:값}여러개의 데이터를 보낼 수도 있음
                
                data:{u_id:u_id},
                            
                success:function(data){
                    $(".id_txt").html(data);
                },
                // 성공하면 위의 데이터 값이 넘어옴

                error:function(){
                    $(".id_txt").html("ERROR");
                }
                //실패하면 "ERROR" 메시지 띄움

            });
            // ajax 종료 
            //위의 형태는 jQuery ajax의 기본

    });

});
</pre>
<br>

<hr>

<br>

###### php페이지에서 검사할 값 가져오기

<br>
<pre>
< ?php
//이전 페이지에서 값 가져오기

$u_id = $_POST[" u_id"];

//DB 연결
include " inc/dbcon.php";

//쿼리
$sql = "select u_id from members where u_id='$u_id';";

//쿼리 보내기
$result = mysqli_query($dbcon, $sql);

//값 받기
$num = mysqli_num_rows($result);
? >
</pre>

<br>

여기서 제이쿼리로 보낼 코드를 작성해야 한다.

<br>
<pre>
< ?php
//이전 페이지에서 값 가져오기

$u_id = $_POST[" u_id"];

//DB 연결
include " inc/dbcon.php";

//쿼리
$sql = "select u_id from members where u_id='$u_id';";

//쿼리 보내기
$result = mysqli_query($dbcon, $sql);

//값 받기
$num = mysqli_num_rows($result);



$return_val = "";
if(!$num){
    $return_val = "사용할 수 있는 아이디입니다.";
} else {
    $return_val = "사용할 수 없는 아이디입니다.";
};

echo $return_val;


? >
</pre>
<br>

###### function을 onclick이 아니라 keyup으로 바꾸면

**keyup()**<br>
 키보드에서 손을 뗄 때 실행하는 함수이기 때문에   
 글자를 입력 할 때 마다 result가 바뀐다.  
 버튼을 클릭하지 않아도 계속 검사가 이루어지고 있는 상태로 브라우저에 부하가 올 수 있다.  