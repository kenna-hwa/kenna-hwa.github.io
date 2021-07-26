---
layout: post
title:  "[Github] error: RPC failed; curl 55 Send failure: Connection was aborted"
author: Kenna
date:   2021-07-26 21:26:35 +0830
image: https://images.unsplash.com/photo-1593720219276-0b1eacd0aef4?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1343&q=80
rating: 43
description: Github 에러 메시지 확인
categories : Github
tags: Github
---

###### error: RPC failed; curl 55 Send failure: Connection was aborted

이 오류는 `http.postBuffer` 값 보다 큰 데이터 양을 전송할 때 발생  
`http.postBuffer`의 크리를 늘리는 꼼수로 데이터를 보낼 수 있다.  

<br>

**git config --global http.postBuffer 524288000**

<br>
이렇게 하면 25mb 이상을 한번에 업로드 할 수 있다.