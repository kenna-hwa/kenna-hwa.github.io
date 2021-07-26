---
layout: post
title:  "[Github] error: RPC failed; curl 55 Send failure: Connection was aborted"
author: Kenna
date:   2021-07-26 21:26:35 +0830
image: https://images.unsplash.com/photo-1556075798-4825dfaaf498?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=755&q=80
rating: 43
description: Github 에러 메시지 확인
categories : Github
tags: Github
---


최근 포트폴리오 작업하면서 거의 밤을 새다시피 코딩하다가 자는 바람에 깃허브에 커밋이 전혀 안올라가고 있다는 사실을 오늘에서야 알았다.  
<br>

파악한 정보로는  

 1) 급한대로 push 하고 잔다고 bash나 터미널, vscode를 넘나들면서 `push`를 해서 main 브랜치가 두개로 나뉘었다.  정확하게 생성된건 아니고 임시 브랜치? 같은 모양새로 main과 origin/main이 구분되고 있었음;  
이도 정확하지 않은게 로컬이 main 이고 원격이 origin/main 같은데 origin/main 이 멈춰있으니 자꾸 `pull` 하라는 메시지가..  

<br>

 2) 그리고 디자인 작업하던 psd 파일이 그만 커밋되는 바람에 심지어 그것도 오늘에서야 발견하는 바람에  
psd 파일 용량이 너무 커서 커밋이 원격으로 `push`가 전혀 안되고 있던 것

<Br>

이 문제를 해결하기 위해 브랜치 머지도 해보고, pull 도 땡겨보고... 삭제도 해보고... 파일 삭제도 해보고...  
근데 이미 저 psd파일이 들어왔다 나갔다 한 기록이 그대로 커밋되어서 그런지
커밋 내역을 `hard`로 다 밀어버리기 전까지는 push가 안될 모양이더라..

<br>
어차피 커밋 밀어버릴바에 새 레포지토리를 만들어서 데이터라도 온전하게 가져가야겠다 싶어서  
(혹시 동기화되어서 수정해놓은 코드 날아갈까봐..)

그냥 새 레포지토리를 만들어서 이전함 ^^^^

<br>


아래는 파일 용량때매 나타난 오류 메시지 해결 방법!


###### error: RPC failed; curl 55 Send failure: Connection was aborted


이 오류는 `http.postBuffer` 값 보다 큰 데이터 양을 전송할 때 발생  
`http.postBuffer`의 크리를 늘리는 꼼수로 데이터를 보낼 수 있다.  

<br>

**git config --global http.postBuffer 524288000**

<br>
이렇게 하면 25mb 이상을 한번에 업로드 할 수 있다.  