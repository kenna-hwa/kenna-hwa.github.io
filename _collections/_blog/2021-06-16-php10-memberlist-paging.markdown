---
layout: post
title:  "[PHP] 회원정보 페이지에 paging 만들기"
author: Kenna
date:   2021-06-16 12:26:35 +0830
image: https://images.unsplash.com/photo-1611647832580-377268dba7cb?ixid=MnwxMjA3fDB8MHxzZWFyY2h8OHx8cGhwfGVufDB8fDB8fA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60
rating: 27
description: 수업 복습
categories : PHP
tags: PHP
---

###### PHP
[PHP 공식 홈페이지]("https://www.php.net/")


###### 회원정보 페이지에 paging 만들기

이전에 만들어둔 list.php 파일에 회원정보 테이블을 paging 시킨다.

<br>

**1. 필요한 데이터들 변수에 담기**
<br>
<br>


**- 전체 데이터 개수 구해서 변수에 담기**
<br>
<br>

<pre>
< ?php
$num = mysqli_num_rows($result);
? >
</pre>
<br>
**- 한 페이지당 글의 개수 설정하고 변수에 담기**
<br>
<br>

<pre>
< ?php
$list_num = 5;
? >
</pre>
<br>

**- 한 블럭 당 페이지 개수 설정하고 변수에 담기**
<br>
<br>

<pre>
< ?php
$page_num = 3;
? >
</pre>
<br>

**- 현재 페이지가 몇 번째 페이지인지 구하기(조건연산자)**
<br>
<br>

<pre>
< ?php
$page = isset($_GET["page"])? $_GET["page"] : 1;
//받아오는 page는 url에 표시되는 숫자로 page가 1과 양의 정수가 아니면 표시되지 않도록 설정
? >
</pre>
<br>

**- 전체 페이지 수 구하는 수식**<br>
**전체 페이지 수  = 전체 데이터 수 / 페이지 당 데이터 개수**<br>
<br>

여기에서 숫자 관련 함수 사용   
  
　· ceil : 올림값. 소수점이 나오면 무조건 올림!  
　· floor : 내림값. 소수점이 나오면 무조건 내림!   
　· round : 반올림. 0.4까지 내리고 0.5부터 올린다.   
<br>

<pre>
< ?php
//1.4처럼 나머지가 나와도 2페이지에 표시해야 하기 때문에 올림
$total_page = ceil($num / $list_num);
? >
</pre>
<br>
<br>
<hr>

<br>

**2. 블럭 설정하기**
<br>
블럭은  < 1 2 3 >    < 4 5 6 > 처럼 페이지를 넘기는 숫자 집합을 말한다.

<br>
<br>

**- 총 블럭의 개수 구하는 수식**<br>
**총 블럭 수 = 전체 페이지 수 / 블럭 당 페이지 수**
<br>
<br>

<pre>
< ?php
$total_block = ceil($total_page / $page_num);
? >
</pre>
<br>

**- 현재 블럭 번호 구하는 수식**<br>
**현재 블럭 번호 = 현재 페이지 번호 / 블록 당 페이지 수**
<br>
<br>
<pre>
< ?php
$total_block = ceil($total_page / $page_num);
? >
</pre>
<br>

**- 블럭 당 시작페이지 번호 수식**<br>
**블럭 당 시작 페이지 번호 = (해당 글의 블럭 번호 - 1) * 블럭 당 페이지 수 + 1**
<br>
<br>
여기에 0보다 작으면 무조건 0을 표시하도록 조건문을 추가한다.
<br>
<pre>
< ?php
$s_pageNum = ($now_block - 1) * $page_num + 1;
if ($s_pageNum <= 0){
    $s_pageNum = 1;
};
? >
</pre>
<br>

**- 블럭 당 마지막 번호 구하는 수식**<br>
**블럭 당 마지막 페이지 번호 = 현재 블럭 번호 * 블럭 당 페이지 수**
<br>
<br>

여기에 마지막 번호가 전체 페이지 수를 넘지 않도록 조건문을 추가한다.
<br>
<pre>
< ?php
$e_pageNum = $now_block * $page_num;
if($e_pageNum > $total_page){
    $e_pageNum = $total_page;
};
? >
</pre>
<br>
<br>
<hr>
<br>

###### paging 할 수 있도록 출력 쿼리 설정
<br>

이전에 만들어둔 list.php 파일에 회원정보 테이블을 paging 시킨다.


<br>
paging은 while문 바로 위에서 시작한다.  
한 개의 페이지에 5개의 데이터를 뿌리면  
  
1페이지에는 1부터 5번까지의 데이터  
2페이지에는 6번부터 10번까지의 데이터가 나타나야 한다.  
<br>

**- 시작 글(회원) 번호 구하는 수식**<br>
**시작 글(회원) 번호 = (현재 페이지 번호 - 1) * 페이지 당 보여질 데이터 수**
<br>
<br>
데이터의 순서는 0부터이기 때문에 1을 빼준다.
<br>
<pre>
< ?php
$start = ($page - 1) * $list_num;
? >
</pre>
<br>

**- 뿌려줄 데이터의 조건 설정해서 가져오기**
<br>
<br>
<pre>
< ?php
$sql = "select * from members limit $start, $list_num;";
//limit로 시작 글 번호 부터 한 페이지 당 글 개수(위에서 $list_num에 담아둠)만큼 출력되도록 함
//기존의 select문을 가져와서 변형시킨다.
//이 $sql로 테이블에 데이터도 뿌린다.

$result = mysqli_query($dbcon, $sql);
//데이터베이스에 쿼리 보내서 가져오기
? >
</pre>
<br>

**- 시작하는 글(회원) 번호 뿌려주기**
<br>
<br>
데이터의 순서는 0부터이기 때문에 빼준 1을 다시 더해 테이블에 뿌린다.
<br>
<pre>
< ?php
$cnt = $start + 1;
? >
</pre>
<br>

**- 테이블의 $array["idx"]를 시작하는 회원 번호로 수정**
<br>
<br>
기존에 array로 받아온 값 array["idx"]를 위에서 설정한 $cnt로 수정한다.
<br>
<pre>
< ?php
        // < td>< ?php echo array["idx"]; ? >< /td> 이것을 아래와 같이 수정
        < td>< ?php echo $cnt; ? >< /td>
? >
</pre>
<br>

**- $cnt 반복문 안에서 1씩 증가**

<br>
$cnt은 글(회원) 시작 번호이기 때문에 반복문에서 하나씩 증가해서 값을 가져와야 한다.  
따라서 $cnt의 값은 1씩 증가해야한다.
<br>

<pre>
< ?php
        //테이블 상단 코드
                while ($array = mysqli_fetch_array($result)){
? >
            < tr>
            <!-- < td><?php //echo $array["idx"]; ?>< /td> -->
                < td>< ?php echo $cnt; ?></ td>

                < td>< ?php echo $array["u_name"]; ?>< /td>
                < td>< ?php echo $array["u_id"]; ?>< /td>
                < td>< ?php echo $array["mobile"]; ?>< /td>
                < td>< ?php echo $array["email"]; ?>< /td>
                < td>< ?php echo $array["birth"]; ?>< /td>
                < td>
                    < ?php echo $array["postalcode"]; ?>
                    < ?php echo $array["addr1"]; ? >
                    < ?php echo $array["addr2"]; ?> 
                < /td>
                < td>< ?php echo $array["reg_date"]; ?></td>
                < td>< a href="edit.php?g_idx=< ? php echo $array["idx"]; ? >">수정< /a>< /td>
                < td>< a href="#" onclick='del_mem(< ? php echo $array["idx"]; ? >)'>삭제< /a>< /td>
            < /tr>

< ?php 
        $cnt = $cnt + 1;
        }; 
? >

</pre>

<br>


###### 페이저 pager 만들기

이제 url을 가지고 페이지를 이동시킬 수 있다.  
아래 pager 블럭을 만들어 페이지를 넘길 수 있도록 UI를 만든다.

<br>

**1. HTML 코드 만들기**
<br>
<br>
클릭해 넘어갈 수 있도록 a로 링크를 만든다.  

<pre>
< p>
        < a href="#">이전< /a>

        < a href="#">다음< /a>
< /p>

</pre>
<br>

**이전과 다음에 url 연결하기**
<br>
<br>
a href에 url을 넣을 때 page번호로 이동하기 때문에 GET 방식으로 이동할 수 있도록 링크를 넣는다.

<pre>
< p>
        < a href="list.php?page=< ?php echo ($page-1); ? >">이전< /a>

        < a href="list.php?page=< ?php echo ($page+1); ?>">다음< /a>
< /p>
</pre>
<br>
다만 이 때 페이지 번호가 1이었을 떄 이전을 눌러 1 미만의 수가 되거나  
최종 페이지에서 다음을 눌러 최종 페이지 수 보다 크게 가면 해당 페이지가 없기 때문에  
조건문을 통해 1보다 작거나 최종 페이지 수 보다 클 때는 페이지를 이동하지 못하도록 한다.  
<br>
<pre>
< p>
        < ?php
        if($page <= 1){ //페이지 수가 1보다 작을 때
        ? >
        < a href="list.php?page=1">이전< /a>
        < ?php }else{ ? >
        < a href="list.php?page=< ?php echo ($page-1); ? >">이전< /a>
        < ?php }; ?>



        < ?php
        if($page >= $total_page){
        ? >
        < a href="list.php?page=<?php echo $total_page; ?>">다음< /a>
        < ?php } else{ ? >
        < a href="list.php?page=< ?php echo ($page+1); ? >">다음< /a>
        < ?php }; ? >
< /p>
</pre>
<br>

**2. 숫자 블럭 만들기**
<br>
<br>

**- 이전과 다음 사이에 숫자 블럭 삽입하기**
<br>
<br>
이전과 다음 사이에 클릭 할 수 있도록 숫자 블럭을 삽입한다.  
< 1 2 3 >  
< 4 5 6 >  
과 같은 블럭을 넣기 위해서는 반복문으로 숫자와 링크를 같이 뿌려줘야 한다.  
이 때 위에서 만든 시작 페이지 변수와 마지막 페이지 변수를 사용한다. ($s_pageNum, $e_pageNum)
<br>
<pre>
< p>
        < ?php
        if($page <= 1){ //페이지 수가 1보다 작을 때
        ?>
        < a href="list.php?page=1">이전< /a>
        <?php }else{ ?>
        < a href="list.php?page=< ?php echo ($page-1); ? >">이전< /a>
        < ?php }; ?>

            < ?php
            //시작 페이지부터 마지막 페이지까지
            //시작 페이지부터 ; 마지막 페이지까지 ; 1개씩 증가한다.
            for($print_page =  $s_pageNum; $print_page < = $e_pageNum; $print_page++){
            ? >
             < a href="list.php?page=< ?php echo $print_page; ? >">< ?php echo $print_page; ?> /a>
            < ?php }; ? >


        < ?php
        if($page >= $total_page){
        ? >
        < a href="list.php?page=< ?php echo $total_page; ? >">다음< /a>
        < ?php } else{ ? >
        < a href="list.php?page=< ?php echo ($page+1); ? >">다음< /a>
        < ?php }; ? >
< /p>
</pre>
<br>
