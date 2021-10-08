---
layout: post
title:  "[Github] git pull과 clone의 차이"
author: Kenna
date:   2021-10-06 11:26:35 +0830
image: https://images.unsplash.com/photo-1556075798-4825dfaaf498?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=755&q=80
rating: 62
description: git pull과 clone의 차이
categories : Github
tags: Github
---

회사 노트북이랑 집에 있는 노트북이랑 두 개를 번갈아가면서 쓰는데  
로컬에서 번갈아 올리면 git pull로 땡겨와야 하는지 git clone으로 땡겨와야 하는지 헷갈려서 정리  

<br>

회사에서 작업한 것을 깃헙 연결(`git init` -> `git remote add origin url` -> `git push origin master`) 해주고  
집에 가서는 `git clone url` 해서 전체 파일을 가지고 오면 된다.  
이 때 리모트 설정도 자동으로 되기 때문에 다운로드 버튼 말고 `git clone url` 하는게 편하다.  
(처음엔 push 말고 다른거 다 무서워서 깃헙에서 다운로드해서 다시 git init 해서 연결했었다.)  
그리고 집에서 작업해서 다시 `git push` 해주고 회사에 가면 `git pull`해서 <b>업데이트 된 사항을 다운로드</b> 해주면 된다.  

반드시 연결된 레포지토리는 같아야하므로 `git remote -v`해서 설정된 주소를 확인!  

결론은   
레포지토리를 처음 땡겨올때만 `git clone url`을 쓰고  
다음부터는 양쪽에서 `git pull (origin main)` 으로 업데이트 된 사항을 가지고 오면 된다.