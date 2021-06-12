---
layout: post
title:  "[MySQL] MySQL Basic"
author: Kenna
date:   2021-05-27 11:26:35 +0830
image: https://images.unsplash.com/photo-1621570360476-a0c6945ebb79?ixid=MnwxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1267&q=80
rating: 10
description: 수업 복습
categories : [MySQL]
tags: [MySQL]
---

###### MySQL
[MySQL 공식 홈페이지]("https://www.mysql.com/")

###### 데이터베이스

데이터를 저장하는 공간 (폴더와 비슷)<BR>
페이지 전체가 아니라 값만 저장해야 관리가 쉽다.

**DBMS**<br>

데이터베이스 매니지먼트 시스템 DATABASE MANAGEMENT SYSTEM<BR>
ex) ORACLE, MS-SQL, MY-SQL, MONGODB, MARIADB 등

MY-SQL은 RDBMS(Relational DataBase Management System)
<pre>
<STRONG>
DBMS   -   DATABASE   -   TABLE   -   DATA<BR>
 OS    -    FOLDER    -   FILE    -   TEXT
 </STRONG>
 </pre>
<BR>



데이터베이스의 표 최상단(1행)에는 Column Name이 있어야 한다.

![데이터베이스 테이블의 형태](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Ftse4.mm.bing.net%2Fth%3Fid%3DOIP.qdziv9QqoVNmnrBdKQDxGwHaE4%26pid%3DApi&f=1)

데이터베이스의 데이터는 테이블의 행row 단위로 저장된다.<BR>
이 행을 record라고 부른다.

각 행에는 **고유한 값**이 필요하다 (id 처럼)<BR>
이것을 **주 키 Primary key**라고 한다.

###### 쿼리 작성 
- 테이블 이름 : 영문 소문자만 쓰는 것이 좋다. (대문자, 언더스코어, 숫자 가능하지만 영문 소문자만 쓰는 것이 best)
- 필드 이름 : 테이블 이름과 같다.
- 일련번호 : 자동 증가하는 회원번호와 같이 auto-increment로 중복 없이 자동 증가되는 필드가 필요하다.
- 비밀번호 : 비밀번호 필드에는 암호화를 시켜야 한다.
- 작은따옴표 : 문자열에는 반드시 작은 따옴표를 사용해야 한다. '' 숫자에는 따옴표를 쓰지 않는다.
- 대소문자 구분 없음 : 대소문자는 구분할 필요는 없지만 가독성을 위해 쿼리는 대문자로 작성하는 것을 추천한다.

<BR>

###### 쿼리 구분

- **DCL(데이터 제어어)** : 생성, 삭제에 관여 GRANT, REVOKE
- **DDL(데이터 정의어)** : 데이터 공간에 관여 CREATE, ALTER, DROP, TRUNCATE
                            데이터를 담는 그릇 즉, 오브젝트를 정의하는 언어로
                            오브젝트는 스키마, 도메인, 테이블, 뷰, 인덱스가 있다.
- **DML(데이터 조작어)** : 데이터에 관여 INSERT UPDATE DELETE SELECT

<BR><BR>
 
**+W3C 스터디 추가**
<br>

###### 가장 중요한 SQL 명령

- SELECT : 데이터베이스에서 데이터 추출(SELECT FROM, SELECT DISTINCT)
- UPDATE : 데이터베이스에서 데이터 업데이트
- DELETE : 데이터베이스에서 데이터 삭제
- INSERT INTO : 데이터베이스에 새 데이터 삽입
- CREATE DATABASE : 새 데이터베이스 생성
- ALTER DATABASE : 데이터베이스 수정
- CREATE TABLE : 새 테이블 생성
- ALTER TABLE : 테이블 수정
- DROP TABLE : 테이블 삭제
- CREATE INDEX : 인덱스(색인) 생성(검색 키 생성)
- DROP INDEX : 인덱스 삭제

<br>

###### WHERE절

<pre>
SELECT 필드명 FROM 테이블명
WHERE 조건문;
</pre>

**제외하고**<br>
<pre>
SELECT 필드명 FROM 테이블명
WHERE NOT 조건문;
</pre>

**그리고**<br>
<pre>
SELECT 필드명 FROM 테이블명
WHERE 조건문
AND 조건문;
</pre>

**또는**<br>
<pre>
SELECT 필드명 FROM 테이블명
WHERE 조건문
OR 조건문;
</pre>
<br>


**WHERE절의 연산자**<br>
- = : 같은
- &gt; : 보다 큰
- &lt; : 보다 작은
- &gt;= : 보다 같거나 큰
- &lt;= : 보다 같거나 작은
- <> : 같지 않은 (SQL에서는 !=을 쓰지 않는다.
- BETWEEN : 범위 내
- LIKE : 패턴에 맞춰 검색
- IN : 여러 개의 조건을 지정할 때
<br><BR>

###### ORDER BY

**ACS** : 오름차순 - 기본값<br>
**DESC** : 내림차순<br>

**오름차순**<br>
<pre>
SELECT 필드명 
FROM 테이블명
ORDER BY 필드명 (ACS);
</pre>

**내림차순**<br>
<pre>
SELECT 필드명 
FROM 테이블명
ORDER BY 필드명 DESC;
</pre>
<br>

**여러 필드명으로 정렬**<br>
<pre>
SELECT 필드명 
FROM 테이블명
ORDER BY 필드명, 필드명;
</pre>
<br>

**여러 필드명에 순서를 정해 정렬**<br>

<pre>
SELECT 필드명 
FROM 테이블명
ORDER BY 필드명 ASC, 필드명 DESC;
</pre>
<br><BR>

###### INSERT INTO

테이블에 새로운 레코드(행)을 삽입
모든 열에 값을 추가하는 경우 열 이름 지정하지 않고 **순서에 맞게** 작성
<br>

<pre>
INSERT INTO 테이블명 (
    필드명1, 필드명2, 필드명3
)
VALUES (
    데이터1, 데이터2, 데이터3
);
</pre>
<br>

###### NULL

필드에 값이 없는 경우 NULL로 표시된다.
<br>

**IS NULL 로 빈 값 찾기**<br>

<pre>
SELECT 필드명 
FROM 테이블명
WHERE 필드명 IS NULL;
</pre>
<br>

**IS NOT NULL 로 비어있지 않은 값 찾기**<br>

<pre>
SELECT 필드명 
FROM 테이블명
WHERE 필드명 IS NOT NULL;
</pre>
<br>

###### UPDATE

테이블의 기존 레코드들을 수정한다.
<br>

<pre>
UPDATE 테이블명
SET 필드명 = 데이터1, 데이터2, 데이터3...
WHERE 조건;
</pre>
<BR>
여기서 WHERE는 업데이트 해야 하는 레코드를 지정하는데 일련번호 같이 주 키로 이용하는 레코드를 지정한다.<BR>
이 WHERE문을 빼먹으면 테이블의 모든 레코드가 업데이트 된다.

###### DELETE

테이블의 기존 레코드들을 삭제한다.
<br>

<pre>
DELETE FROM 테이블명
WHERE 조건;
</pre>
<BR>
여기서도 WHERE문을 빼먹으면 **모든 레코드가 삭제된다.**

