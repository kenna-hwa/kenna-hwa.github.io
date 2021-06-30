---
layout: post
title:  "[React] React - 컴포넌트 제작"
author: Kenna
date:   2021-06-30 21:26:35 +0830
image: https://images.unsplash.com/photo-1593720219276-0b1eacd0aef4?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1343&q=80
rating: 32
description: 인프런 - 생활코딩 React 수업
categories : React
tags: React
---

###### React
[Inflearn 생활코딩]("https://www.inflearn.com/course/react-%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9/dashboard")


###### 리액트가 없다면

리액트가 없는 상황   
   
public 디렉토리는 create-react-app 에서 `npm run start` 했을 때  
파일을 찾는 document root 다.   
   
   <br>

###### 컴포넌트 만들기 1

<pre>
//컴포넌트 만드는 코드 
class App extends Component {
  render() {
    return (
      < div className="App">
        Hello React!!
      < /div>
    );

  }
}
</pre>

위 코드는 App 이라는 클래스를 만들고 리액트의 컴포넌트 클래스를 상속해서 새로운 클래스를 만드는 것.  
이 클래스는 render 라는 메소드를 가진다.   
   
like Templet!   
   
subject라는 태그를 만들어 보자.  
<br>

<pre>
// 1 Subject 라는 클래스 생성
// 클래스 이름은 대문자로 시작한다.

class Subject extends Component {


  
}
</pre>

<pre>
// 2 렌더 함수 필요

class Subject extends Component {
  render() {



  }
}
</pre>

<pre>
// 3 render 함수 안에 return 을 넣어준다.
// 클래스 안에 들어가 있는 함수는 function 을 생략한다!

class Subject extends Component {
  render() {
    return();


  }
}
</pre>

<pre>
// 4 html 코드를 return 안에 넣어준다.
// 컴포넌트는 반드시 하나의 최상위 태그로 시작해야 한다.

class Subject extends Component {
  render() {
    return(
    < header>
        < h1>WEB< /h1>
         world wide web!
      < /header>
    );
  }
}
</pre>

<pre>
// 5 기존 App 컴포넌트에 Subject를 넣어준다.

class App extends Component {
  render() {
    return (
      < div className="App">
        < Subject>< /Subject>
      < /div>
    );

  }
}
</pre>

해당 부분을 개발자 도구로 확인해보면 글자에 < header> 태그가 생성되어 표시된다.   
웹 브라우저는 react를 모른다.   
react가 최종적으로 웹 브라우저에게 HTML 코드를 공급해주기 때문이다!   
<br>

App.js는 유사 자바스크립트다.   
태그를 표현하는 부분에 따옴표나 역슬래시도 작성하지 않았다.  
자바스크립트와 비슷하지만 자바스크립트 신택스Syntax는 아니다.   
react는 페이스북에서 만든 jsx다.   
이 jsx를 작성하면 create-react-app 이 알아서 converting 해주는 것.   

<br>

###### 컴포넌트 만들기 2

기존에 만들었던 다른 HTML 태그들도 Component를 만들어 본다.   

<pre>
class TOC extends Component {
  render() {
    return(
      < nav>
      < ul>
          < li>< a href="1.html">HTML< /a>< /li>
          < li>< a href="2.html">CSS< /a>< /li>
          < li>< a href="3.html">JavaScript< /a>< /li>
      < /ul>
      < /nav>
    );
  }
}
</pre>

<pre>
class Content extends Component {
  render() {
    return(
      < article>
      < h2>HTML< /h2>
      HTML is Hypertext Markup Language.
      < /article>

    );
  }
}
</pre>

이렇게 만들면 아래와 같이 App 컴포넌트에 넣어 원래의 HTML 문서처럼 만들 수 있다.  

<pre>
class App extends Component {
  render() {
    return (
      < div className="App">
        < Subject>< /Subject>
        < TOC>< /TOC>
        < Content>< /Content>
      < /div>
    );

  }
}
</pre>
<br>

**컴포넌트는 정리하는 도구**<br>
컴포넌트의 이름에 집중하게 됨으로써 복잡도가 확! 낮아지게 되었다.   

<br>

###### props

이런 리액트 코드를 패키지로 만들면 다른 사람들이 다운 받아서 사용할 수 있다.   
   
우리가 이미 알고 있는 태그 중 a 태그처럼 속성을 가지는 태그들이 있다.   
태그의 이름이라는 공통점과 속성이라는 차이점을 통해서 재사용성이 높아진다.   
  
내가 만든 react 컴포넌트에도 속성을 적용하면 더 사용성이 높아질 것 같다.   
      
[React 공식 문서 - Components와 Props]("https://ko.reactjs.org/docs/components-and-props.html")    
   
<pre>
class Welcome extends React.Component {
  render() {
    return < h1>Hello, {this.props.name}< /h1>;
  }
}
</pre>
이렇게 만든다.   
<br>

기존에 만들었던 Subject 태그의 Web 이라는 글자가 태그 안에서 변경될 수 있도록 만든다.  
중괄호를 사용한다.   
this를 사용한다.
{ this.props.속성 } - props는 태그의 attribute 라는 뜻이다.   
   
아래와 같이 적용할 수 있다.   

<pre>
class Subject extends Component {
  render() {
    return(
    < header>
        < h1>{this.props.title}< /h1>
        {this.props.sub}
      < /header>
    );
  }
}

class App extends Component {
  render() {
    return (
      < className="App">
        < Subject title="Web" sub="world wide web!">< /Subject>
        < Subject title="React" sub="For UI">< /Subject>
        < TOC>< /TOC>
        < Content>< /Content>
      </ div>
    );

  }
}

export default App;
</pre>

<br>

###### React Developer Tools
   
설명서를 볼 줄 압시다.  
현재 상태를 측정합시다.  

다른 사람에게 질문하고, 검색하자.   

개발자도구와 같은 크롬의 **React-Developer-Tools**  <br>
[크롬 웹 스토어]("https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=ko")  

<br>

###### Component 파일로 분리하기
  
지금까지 만든 컴포넌트를 정리하여 재사용성을 높인다.  
별도의 파일로 정리정돈   
<br>

src > component라는 폴더를 만든다.    
TOC.js 라는 파일을 만들어 기존에 만들어 둔 TOC 컴포넌트를 넣는다.   

  

<pre>
class TOC extends Component {
  render() {
    return(
      < nav>
      < ul>
          < li>< a href="1.html">HTML< /a>< /li>
          < li>< a href="2.html">CSS< /a>< /li>
          < li>< a href="3.html">JavaScript< /a>< /li>
      < /ul>
      < /nav>
    );
  }
}
</pre>
  
위와 같이 붙여넣으면 Component가 정의되지 않았다는 메시지가 나온다.  
Component를 import 시켜준다.  
  
<pre>
import React, { Component } from 'react';

class TOC extends Component {
  render() {
    return(
      < nav>
      < ul>
          < li>< a href="1.html">HTML< /a>< /li>
          < li>< a href="2.html">CSS< /a>< /li>
          < li>< a href="3.html">JavaScript< /a>< /li>
      < /ul>
      < /nav>
    );
  }
}
</pre>

React 라이브러리에서 Component를 로딩해온다.  
이 코드는 꼭 넣어준다고 생각하자.   

TOC 안에 많은 함수 등등 중에서 외부에 사용할 것들을 골라낼 수 있다.  
`export default TOC;`<br>
를 넣어준다.  
  
이제 App.js에 TOC.js 파일을 import 시켜준다.   


`import TOC from './components/TOC';`

이렇게 하면 컴포넌트를 파일로 쪼갤 수 있다.  
<br>
