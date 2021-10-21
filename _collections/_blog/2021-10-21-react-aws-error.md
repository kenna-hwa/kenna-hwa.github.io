---
layout: post
title:  "[React] AWS 튜토리얼에서의 오류"
author: Kenna
date:   2021-10-21 22:26:35 +0830
image: https://images.unsplash.com/photo-1591267990439-bc68529677c3?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1336&q=80
rating: 64
description: AWS API와 상호 작용하는 프론트엔드 코드 작성 오류
categories : React
tags: React
---

###### AWS 튜토리얼에서의 오류

<br>

[오류가 있는 부분]("https://aws.amazon.com/ko/getting-started/hands-on/build-react-app-amplify-graphql/module-four/?e=gs2020&p=build-a-react-app-three")

<br>

AWS 공부하고 있는데 모듈 4 코드를 다 쳤는데,  
오탈자 확인도 했는데,  
`npm start`가 안 먹어서 오류 메시지를 검색했더니  
(오류 메시지 : 'createNote' is not exported from './graphql/mutations' (imported as 'createNoteMutation')
아래 스택오버플로우와 같은 답변이 나왔다.  
공식문서인데... 믿었는데 공식문서....

<br>


```
//공식문서 리액트 코드 

import { listNotes } from './graphql/queries';
import { createNote as createNoteMutation, deleteNote as deleteNoteMutation } from './graphql/mutations'
```
<br>

🔽🔽🔽
<br>

```
//스택오버플로우 보고 수정한 리액트 코드

import { listTodos as listNotes } from './graphql/queries';
import { createTodo as createNoteMutation, deleteTodo as deleteNoteMutation } from './graphql/mutations';
```

<br>

<br>

[참고한 스택오버플로우]("https://stackoverflow.com/questions/65524754/attempted-import-error-createnote-is-not-exported-from-graphql-mutations")

<br>
<br>
