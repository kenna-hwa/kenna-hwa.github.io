---
layout: post
title:  "[React] React - 이벤트"
author: Kenna
date:   2021-07-03 15:26:35 +0830
image: https://images.unsplash.com/photo-1593720219276-0b1eacd0aef4?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1343&q=80
rating: 35
description: 인프런 - 생활코딩 React 수업
categories : React
tags: React
---

###### React
[Inflearn 생활코딩]("https://www.inflearn.com/course/react-%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9/dashboard")



###### 이벤트 state props 그리고 render 함수

애플리케이션을 역동적으로 만들어주는 event 사용해보자.  
props, state, event가 서로 상호작용하면서 애플리케이션을 역동적으로 만든다.  
  
<br>
  
해야할 일!   
<br>
  
1. 제목 WEB에 링크를 달아서 클릭하면 welcome 메시지가 나오게 하자.   
2. 아래 li 링크들을 클릭하면 해당 언어의 설명이 아래에 나오게 하자.  
  


**첫 번째**

<br>
Subject.js에서 h1에 link 태그를 넣어준다.  
<pre>
import React, { Component } from 'react';


class Subject extends Component {
    render() {
      return(
      < header>
          < h1>< a href="/">{this.props.title}< /a>< /h1>
          {this.props.sub}
        < /header>
      );
    }
  }

  export default Subject;
</pre>
<br>
  
이제 화면의 링크를 클릭하면 App 컴포넌트의 state가 바뀌고  
바뀐 state가 < Content>< /Content> 컴포넌트의 props의 값으로 전달됨으로써 동적으로 애플리케이션이 바뀌는 것을 구현할 수 있다.  
  
  
**state 셋팅하기**  
<br>
어떤 페이지가 welcome 페이지인지 read 페이지(읽기 페이지)인지 알아내기 위해서  
App.js의 constructor 함수의 state에다가 mode라는 값을 준다.  
기본값으로 welcome을 준다.  
그리고 mode가 welcome일 때, content 영역에 표시할 텍스트도 지정해준다.  
  
<br>

<pre>
class App extends Component {
  constructor(props){
    super(props);
    this.state = {
      mode: 'welcome',
      subject:{title:'WEB', sub: 'world wide web!'},
      welcome:{title:'welcome', decs:'Hello, React'},
      contents:[
        {id: 1, title: 'HTML', desc: 'HTML is information...'},
        {id: 2, title: 'CSS', desc: 'CSS is design...'},
        {id: 3, title: 'Javascript', desc: 'Javascript is interactive...'}
      ]
    }
  }
  render() {
    return (
      < div className="App">
        < Subject title={this.state.subject.title} sub={this.state.subject.sub}>< /Subject>
        < TOC data={this.state.contents}>< /TOC>
        < Content title="HTML" desc="HTML is Hypertext Markup Language.">< /Content>
      < /div>
    );

  }
}
</pre>
<br>

state에 대해 알아야 할 또 하나의 사실!  

<br>

react에서는 props나 state의 값이 바뀌면  
그 state를 가지고 있는 컴포넌트의 **render함수가 다시 호출**되고,  
그 render 함수가 다시 호출됨에 따라서 render함수의 하위 컴포넌트가 가진 render 함수들도 다시 호출된다.   
render 함수는 어떤 html을 만들 것인가 하는 기능을 가지고 있다.
<br>

props나 state가 바뀌면 **화면이 다시 그려진다.**
<br>

그럼 mode의 값에 따라서 만들어지는 render 함수의 결과가 달라지도록 **조건문**을 사용한다.  
변수 _title과 _desc를 선언하고 null 값을 준다.  
<br>

<pre>
  var _title, _desc = null;
  render() {
    if(this.state.mode === 'welcome'){

    }else if(this.state.mode === 'read'){
      
    }
  }
</pre>
<br>

그리고 mode가 welcome일 떄는 _title에 this.state.welcome의 title 값이 들어가도록 _title 변수에 할당하고  
return 의 Content 컴포넌트에 title에 _title 변수를 넣는다.
그리고 desc도 할당하고 _desc 변수를 넣는다.  
else if에도 read 를 mode가 read일 때 _title과 _desc를 넣어준다.


<br>

<pre>
class App extends Component {
  constructor(props){
    super(props);
    this.state = {
      mode: 'welcome',
      subject:{title:'WEB', sub: 'world wide web!'},
      welcome:{title:'welcome', decs:'Hello, React'},
      contents:[
        {id: 1, title: 'HTML', desc: 'HTML is information...'},
        {id: 2, title: 'CSS', desc: 'CSS is design...'},
        {id: 3, title: 'Javascript', desc: 'Javascript is interactive...'}
      ]
    }
  }
  render() {
    var _title, _desc = null;
    if(this.state.mode === 'welcome'){
      _title = this.state.welcome.title;
      _desc = this.state.welcome.desc;
    }else if(this.state.mode === 'read'){
      _title = this.state.contents[0].title;
      _desc = this.state.contents[0].desc;
    }

    return (
      < div className="App">
        < Subject title={this.state.subject.title} sub={this.state.subject.sub}>< /Subject>
        < TOC data={this.state.contents}>< /TOC>
        < Content title={_title} desc={_desc}>< /Content>
      < /div>
    );
  }
}

export default App;

</pre>
<br>

console.log로 각 컴포넌트의 render함수를 찍어보면  
App render
Subject render  
TOC render  
Content render  
가 순서대로 찍힌다.  
  
<br>

이 상태에서 mode를 welcome으로 변경하면  
App render가 먼저 돌고  
다시 모든 하위 컴포넌트들이 렌더링 되는 것을 볼 수 있다.  
<br>


###### 이벤트 설치

Subject 컴포넌트를 설치했을 때 App의 mode를 바꾸는 것이 목적  
  
어렵다!!  
  
Subject.js의 내용을 그대로 복사해서 App.js에 붙여넣는다.

<pre>
      < header>
          < h1>< a href="/">{this.props.title}< /a>< /h1>
          {this.props.sub}
      < /header>
</pre>
<br>

이 부분을  
<pre>
return (
      < div className="App">
        {/*< Subject title={this.state.subject.title} sub={this.state.subject.sub}>< /Subject>*/}
        < header>
          < h1>< a href="/">{this.state.subject.title}< /a>< /h1>
          {this.state.subject.sub}
        < /header>
        < TOC data={this.state.contents}>< /TOC>
        < Content title={_title} desc={_desc}>< /Content>
      < /div>
</pre>

이렇게 직접 넣어서 이벤트 프로그래밍을 하고,  
나중에 다시 이 < header>를 Subject 컴포넌트에 넣어주기로 한다.  
<br>

a 링크를 클릭했을 때 어떤 자바스크립트가 실행되도록 하는 이벤트 리스너는  
**onclick**이다.  

리액트는 유사 html 을 만들기 때문에 **onClick**을 쓰고,  
쌍따옴표가 아닌 **중괄호{}**를 쓴다.  
   
 <br>

<pre>
< h1>< a href="/" onClick={function(){
            
          }}>< /a>
< /h1>
</pre>
<br>

이 때, 이 이름이 없는 function 사용자 정의 함수는 링크를 클릭했을 때 실행되도록 약속되어 있다.   
하지만 alert같은 명령어를 넣고 ok를 누르면 페이지가 reload 된다.   
reload 되지 않도록 해야한다!   

a 를 클릭했을 때 href의 주소가 가진 페이지로 이동하게 하는 기본적인 방법 말고 다른 방법을 사용한다.  
  
**onClick 이벤트를 넣었을 때 우리가 만든 function() 괄호 안에 매개변수로 event라고 하는 객체를 주입하기로 약속되어 있다.**
<br>

이것이 **e**이다.   
  
이 e라는 객체에 preventDefault() 함수를 찍어본다.  
preventDefault()는 이벤트가 발생한 태그의 기본적인 동작을 못하게 막는 것이다.  

<br>

이렇게 하면 preventDefault()때문에 페이지가 reload 되지 않는다.  
그래서 이벤트를 걸 때는 기본적인 동작을 못하게 해야할 때 쓰는 preventDefault()를 먼저 걸어줘야 할 때가 있다. 

<br>