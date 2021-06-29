---
layout: post
title:  "[React] React - 개발환경"
author: Kenna
date:   2021-06-29 21:26:35 +0830
image: https://images.unsplash.com/photo-1593720219276-0b1eacd0aef4?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1343&q=80
rating: 31
description: 인프런 - 생활코딩 React 수업
categories : React
tags: React
---

###### React
[Inflearn 생활코딩]("https://www.inflearn.com/course/react-%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9/dashboard")


###### 수업소개

Javascript 객체 지향 수업 먼저 들으면 좋다.   
리액트는 페이스북에서 만든 자바스크립트 UI 라이브러리다.   
한 마디로 정의하기는 쉽지 않다.   
<br>

우리는 복잡한 코드를 **사용자 정의 태그**를 만들어 사용할 수 있다.   
리액트에서는 사용자 정의 태그를 **컴포넌트Component** 라고 부른다.   
<br>

리액트의 컴포넌트는   

<p>

1. 가독성  
2. 재사용성  
3. 유지보수  

</p>

에 강점을 가진다.   
내가 만든 컴포넌트, 남이 만든 컴포넌트를 사용할 수 있는 능력을 가질 수 있다.   

<br>

###### 공부 전략

코딩과 실행을 반복하면서 개발을 해 나간다.   
CODING -> RUN -> DEPLOY   

<br>

###### 개발환경의 종류 

공식 문서에 익숙해지기.   
[리액트 React]("https://ko.reactjs.org/")
<br>

시작하기   

〈 온라인 플레이그라운드 〉   
   
[코드샌드박스]("https://codesandbox.io/s/new")
   
〈 웹 사이트에 React를 추가하기 〉  

이미 만들어져 있는 HTML 문서에 React를 추가하기   
나중되면 어려워질 수 있다.   
   
〈 새 React 앱 만들기 〉   
   
툴체인을 통해 개발 환경을 셋팅할 수 있다.   
추천해주는 앱   
   
Create React App    
[Create React App]("https://github.com/facebook/create-react-app")  
   
〈 설치하기 〉
   
설치하기 위해 npm 이 필요하다.   
node.js를 이용해서 만든 여러 앱을 설치할 수 있도록 만든 도구   
node.js계의 앱스토어 (오호!)   
   
<br>

###### npm을 이용해서 create react app 설치
   
node.js 설치하기   
   
[node.js]("https://nodejs.org")    
설치 후에 cmd에서 `node --version` 쳐서 버전이 뜨면 정상 설치 (윈도우 기준)   
   
터미널에서 `npm install -g create-react-app` 명령어 작성한다.   
-g는 글로벌로 컴퓨터 어디서도 실행할 수 있게 된다.   
 
설치 시 비밀번호를 요구하거나 권한이 없다고 나올 수 있다.   
   
설치 완료 후에는 `create-react-app --version` 으로 설치 확인을 해준다.    
   
npx 는 npm이 프로그램을 설치하는 프로그램이라면 npx는 create-react-app이라는 앱을 딱 한 번 설치하고 지우는 프로그램이다.  
컴퓨터 내의 공간을 낭비하지 않으며, 매번 다운 받기 때문에 새로운 버전을 이용할 수 있다.   
  
<br>

###### create react app을 이용해서 개발 환경 구축

개발 환경을 어느 디렉토리에 셋팅할 것인가?   
<br>

1. 바탕화면에 react-app 폴더를 만든다.(mkdir 해도 된다.) 
2. cmd에서 react-app 폴더로 경로를 이동한다.   
3. `create-react-app .` 이라는 명령어로 react-app 폴더 안에 create-reate-app 개발환경을 설치한다.

<br>

###### 샘플 웹앱 실행

vscode에서 터미널을 이용할 수 있다.   
   
`ctrl+~` 키를 이용해 터미널에서 `npm run start` 를 입력한다.   
어떤 특정한 웹페이지 하나를 보여준다.  
개발 모습을 확인하기 위한 로컬 주소가 나타난다.   
현재 나타나는 모습은 create-reate-app이 가장 최소한의 앱의 모습을 구현해 둔 것이다.   
리액트 기술을 이용한 웹앱이다.      
<br>

실행 종료는 `ctrl+c`   

<Br>

**React 실행**
<br>

실행 : npm run start    
종료 : ctrl + c

<br>

###### JS 코딩하는 법

디렉토리 구조   
<br>

src와 public   
   
public은 index.html 이 있는 곳   
리액트로 만든 컴포넌트들은 < div id="root">< /div> 안에 들어간다.   
id 가 root인 div 안에 들어가는 태그는 src(source)디렉토리 안의 파일들이다.  
앞으로의 대부분 파일은 src 안에 넣게 된다.   
<br>

리액트에 진입하는 파일은  
**index.js**   

이 안에
<pre>

ReactDOM.render(
  < React.StrictMode>
    < App />
  < /React.StrictMode>,
  document.getElementById('root')
);

</pre>
이 부분이 중요하다.   
<br>

< App/> 이 바로 컴포넌트다.   
이 컴포넌트의 실제 구현은 **import**를 통한다.   
이 App 태그는 src 디렉토리 내의 **App.js**이며 이것을 실행한 결과가 현재 랜딩 페이지이다.   
   
App.js 의 return 다음 HTML 코드를 지우고 "Hello, React!!" 라는 메세지를 삽입해본다.   
   
이 떄 리액트는 반드시  
가장 바깥쪽에 태그 하나가 있어야 한다.   

<br>

###### CSS 작성하는 법

create-react-app 의 css 수정하는 법   

**index.css** 를 수정한다.  

import 된 사용자 정의 컴포넌트와 실제 코드 안의 컴포넌트 명은 항상 같아야 하며 대문자로 시작되어야 한다.   
App.js 안의 react 의 컴포넌트가 로드되었을 때 App.css도 같이 로드되어서 디자인을 같이 할 수 있다.   

<br>

###### 배포하는 법

localhost:3000에서 DevTools를 꺼낸다.   
Network를 들어간 후    
새로고침에서 마우스 오른쪽 클릭을 하고 가장 마지막에 `캐시 지우고 강력 새로고침` 을 클릭한다.   
보면 상당히 무거움을 알 수 있다. (1.7MB) 

<br>

빌드 시에는  
`npm run build` 하면 build 파일이 추가된다.   
build 안의 index.html 에는 공백이 하나도 없이 정리된다.   
그래서 실제로 서비스할 때는 bulid 안의 파일을 서비스하면 된다.   
web server의 document root 디렉토리에는 build 안의 파일을 넣으면 된다.   

<br>

**npm을 통해 설치하는 간단한 웹 서버 설치**
<br>

`npm install -g serve` 혹은 `npx serve -s build` 로 서브를 열 수 있는데, serve -s build 하면 build 디렉토리를 root로 하겠다는 뜻이 된다.
   
실행하면 localhost를 알려준다.  
이전의 1.7MB에서 KB 단위로 내려가게 된다.

<br>
