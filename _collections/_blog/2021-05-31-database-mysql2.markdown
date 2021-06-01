---
layout: post
title:  "[MySQL] MySQL Basic2"
author: Kenna
date:   2021-05-31 23:26:35 +0830
image: https://images.unsplash.com/photo-1621570360476-a0c6945ebb79?ixid=MnwxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1267&q=80
rating: 10
description: W3C | MySQL 문서
---

###### MySQL
[MySQL 공식 홈페이지]("https://www.mysql.com/")


###### LIMIT절

반환할 레코드 수를 지정하는데 사용한다.
수천개 중에 몇 개만 골라낼 수 있다.

<pre>
SELECT 필드명 FROM 테이블명
WHERE 조건문
LIMIT 숫자;
</pre>

###### MIN() / MAX() 함수

MIN() 함수는 선택한 열의 가장 작은 값을 반환한다.
MAX() 함수는 선택한 열의 가장 큰 값을 반환한다.

<pre>
SELECT MIN(필드명)
FROM 테이블명
WHERE 조건문;
</pre>

<pre>
SELECT MAX(필드명)
FROM 테이블명
WHERE 조건문;
</pre>

###### COUNT() / AVG() / SUM() 함수

COUNT() 함수는 지정된 기준과 일치하는 행 수를 반환한다.
AVG() 함수는 숫자 열의 평균 값을 반환한다.
SUM() 함수는 숫자 열의 총 합계를 반환한다.

<pre>
SELECT COUNT(필드명)
FROM 테이블명
WHERE 조건문;
</pre>


<pre>
SELECT AVG(필드명)
FROM 테이블명
WHERE 조건문;
</pre>


<pre>
SELECT SUM(필드명)
FROM 테이블명
WHERE 조건문;
</pre>

