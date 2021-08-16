---
layout: post
title:  "[React] 필모그래피 영화 앱 만들기 8"
author: Kenna
date:   2021-08-16 15:26:35 +0830
image: https://images.unsplash.com/photo-1591267990439-bc68529677c3?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1336&q=80
rating: 53
description: React로 영화 앱 만들기
categories : React
tags: React
---
<br>

###### react-router-dom 설치

<br><br>

index 구현 외에 링크를 통해 넘어가는 것을 실행하기 위해 react-router-dom을 설치한다.  
`npm i react-router-dom`로 설치 가능하다.  
네비게이션을 쉽게 구현할 수 있다.  

<br>

**폴더구조 정리하기**

<Br>

만들어 둔 컴포넌트들을 정리해준다.  

`components/`
components 폴더 안에 Movie 컴포넌트를 넣어준다. 

`routes/`  
routes 폴더 안에 라우터로 이동할 다른 폴더를 만들어준다.
여기에서는 `Home.js`, `About.js`을 만든다.  
`Home.js`는 지금까지 만든 `App.js`가 옮겨가고 메인 index 페이지가 된다.


<br>

`App.js` 파일을 복사해서 `Home.js` 파일로 옮긴다.
`Home.js` 파일의 컴포넌트명과 css 파일명을 수정해준다. (App -> Home)

`App.js` 파일을 전부 `Home.js`로 옮기고 나면  
`App.js` 파일을 전부 삭제하고 `Home.js`컴포넌트를 반환하도록 return을 수정해준다.

<br><br>

###### router 만들기  

<br><br>

정리한 App 컴포넌트에 라우터를 넣어준다.  


*라우팅은 일종의 '택배 배송'과 흡사하다.*  
*라우터는 집배소와 같은 개념으로 클라이언트가 ㅁㅁ라고 하는 서버로 택배를 보내려고 하면 우선 내 브라우저가 ARP라는 곳에 대충이라도 주소를 물어보고 1차적으로 주소와 함께 보낸다.*   
*그럼 라우터는 그 주소를 알고 있으면 바로 해당 서버를 보내고 아니면 다음 라우터에 혹시 ㅁㅁ 서버의 주소를 아는지 물어본다.*

<br>

라우터는 이러한 과정을 거쳐서 사용자가 입력한 URL을 통해 특정 컴포넌트를 불러준다.  
리액트에서는 `http://www.sample.test/about` 과 같이 뒤에 슬래시/컴포넌트명 으로 이동한다.  

설치한 react-router-dom 라이브러리에서 **HashRouter와 Route** 두 개의 컴포넌트를 이용한다.   
<br>

```
//수정 전 App.js

import React from 'react';
import Home from './routes/Home'

class App extends React.Component {
render(){
  return <Home />
  }
}
export default App;
```
<br>

수정 전의 코드에서 `Home.js` 컴포넌트를 import한 것은 삭제하고
**HashRouter와 Route** 를 import 한다.  
return 부분에서 `<Home />`은 `<Route />`로 바꾸고 `<HashRouter>` 태그로 감싼다.  
그리고 `<Route />`는 두 가지의 props를 가지는데  
URL을 위한 **path props**와 그 URL에 맞는 컴포넌트를 불러와주는 **component props**를 가진다.  

사용자가 URL로 about이라는 글자를 입력하면 path props가 확인하고, 해당 props에 맞는 component를 찾아주는 과정이다.  
<br>

```
//수정 후 App.js

import React from 'react';
import About from './routes/About';
import { HashRouter, Route } from 'react-router-dom';

class App extends React.Component {
render(){
  return (
  <HashRouter>
  <Route path="/about" component={About} />
  </HashRouter>
)}
}
export default App;
```

그리고 상단에 about 컴포넌트를 import 해준다.  

<br><br>

###### About 컴포넌트 만들기

<br><Br>

```
import React from 'react';


function About() {
    return <span>About this page</span>
}
export default About;
```
<br>
위와 같이 간단한 About 컴포넌트를 만들고  
주소 입력창에 localhost:3000/#/about을 입력해서 페이지가 정상 작동 되는지 알아본다.  

이 라우터들은 추가로 더 만들어 줄 수 있다.  
Home 컴포넌트도 추가로 입력한다.  

<br>

```
import React from 'react';
import { HashRouter, Route } from 'react-router-dom';
import About from './routes/About';
import Home from './routes/Home';

class App extends React.Component {
render(){
  return (
  <HashRouter>
  <Route path="/about" component={About} />
  <Route path="/" component={Home} />

  </HashRouter>
)}
}
export default App;
```

<Br>

그런데 여기까지 입력하면 About 컴포넌트와 Home 컴포넌트가 동시에 나오게 된다.  
<br><br>

###### Route 중첩 문제 해결

<br><Br>

현재 Home 컴포넌트의 path는 `/` 이다.  
그리고 About 컴포넌트는 `/about`이다. 
둘 다 `/`라는 path를 포함하고 있기 때문에 중첩이 이루어 지는 것이다.  
이런 경우 `<Route>`에 **exact props**를 추가해준다.  

```
import React from 'react';
import { HashRouter, Route } from 'react-router-dom';
import About from './routes/About';
import Home from './routes/Home';

class App extends React.Component {
render(){
  return (
  <HashRouter>
  <Route path="/" exact={true} component={Home} />
  <Route path="/about" component={About} />
  </HashRouter>
)}
}
export default App;
```
<br>

지금은 페이지가 두 개 뿐이기 때문에 `/` path를 가진 Home에만 넣었고  
추후 `/about/picture` 과 같이 추가 path가 생기면 각각의 라우터에 넣어주면 된다.  

<br><Br>

###### Navigation 만들기

<br><Br>

`Navigation.js` 파일을 생성하고 간단한 Navigation 마크업을 작성한다.  
<br>

```
import React from 'react';

function Navigation(){
    return (<section>
        <a href="/">Home</a>
        <a href="/about">About</a>
    </section>)
}
export default Navigation;
```
<br>

하지만 현재 상단에 나타나는 Home과 About을 클릭하면  
매번 화면이 깜빡거리는 (새로고침 되는 현상) 문제가 발생한다.  
리액트가 비동기적으로 화면을 다시 받아오는 것이 아니라  
기존의 HTML처럼 현재 문서에서 다른 문서로 넘어가기 위해  
**현재 컴포넌트를 죽이고 다른 컴포넌트를 불러오기 때문**에 그렇다.  

<br>

이 문제를 해결하기 위해 HTML 의 `a` 링크가 아닌  
리액트의 Link 컴포넌트를 사용한다.  
react-router-dom 라이브러리에서 Link 컴포넌트를 사용하기 위해 Link 컴포넌트를 import 한다.  
<br>

```
import React from 'react';
import { Link } from 'react-router-dom';

function Navigation(){
    return (<section>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>  //Link to
    </section>)
}
export default Navigation;
```
<br>

`App.js` 컴포넌트에서 `<Navigation />`은 반드시 `<HashRouter>` 안에 있어야 한다.  
Link 를 사용하는 컴포넌트는 라우터 안에 있어야 하기 때문이다.  


<br>
<br>


