---
layout: post
title:  "[React] React - Create 기능구현"
author: Kenna
date:   2021-07-15 21:26:35 +0830
image: https://images.unsplash.com/photo-1593720219276-0b1eacd0aef4?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1343&q=80
rating: 39
description: 인프런 - 생활코딩 React 수업
categories : React
tags: React
---

###### React
[Inflearn 생활코딩]("https://www.inflearn.com/course/react-%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9/dashboard")


###### create 구현 : mode 변경 기능


TOC와 Content 사이에다가 수정 삭제 버튼을 든다.
<br>

<pre>
        < ul>
          < li>< a href="/create">create< /a>< /li>
          < li>< a href="/update">update< /a>< /li>
          < li>< input type="button">delete< /li>
        < /ul>
</pre>

위와 같이 마크업하고 컴포넌트를 만든다.
<br>

<pre>
//App.js

import Control from './components/Control';

< Control onChangeMode={function(){
          
        }.bind(this)}>< /Control>
</pre>

이제 onChangeMode 라는 핸들러를 넣고  
Control.js에 와서 클릭했을때 onChangeMode 핸들러가 실행되도록 list 각각에 onClick을 삽입한다.    

<pre>
< ul>
    < li>< a href="/create" onClick={function(e){
            e.preventDefault();
            this.props.onChangeMode('update')
    }.bind(this)}>create< /a>< /li>
    < li>< a href="/update">update< /a>< /li>
    < li>< input type="button" value="delete">< /input>< /li>
< /ul>
</pre>

<br>
그러면 App.js에서 첫번째 인자를 받을 수 있어야 하는데 mode라는 첫번째 인자를 받아본다.

<pre>

        < Control onChangeMode={function(_mode){
          this.setState({
            mode:_mode
          })
        }.bind(this)}>< /Control>

</pre>

이렇게 받으면 클릭했을 때 App의 state 중 mode가 create, update, delete로 바뀌는 것을 볼 수 있다.

<br>

###### create 구현 : mode 전환 기능

읽기를 read content라고 바꾸고 쓰기를 create content라고 바꾸자.  
mode가 create가 되면 앱 컴포넌트가 create content가 되도록 하자.  

<br>
기존 Content를 이름을 바꿔본다.  
Content.js 를 ReadContent.js로 변경한다.   
내부의 컴포넌트를 사용한 부분의 이름을 전부 변경한다. (자동 변경 기능도 있다.)  

그리고 ReadContent.js 파일을 복사해서 CreateContent.js 파일을 만든다.  

<br>

App.js에서 아래 Control에 있는 ReadContent 컴포넌트가 mode가 'create'가 되면   
CreateContent가 되도록 코드를 작성한다.  

mode의 값에 따라 Article 영역이 교체되는 코드는  
<pre>
if(this.state.mode === 'welcome'){
      _title = this.state.welcome.title;
      _desc = this.state.welcome.desc;
    }else if(this.state.mode === 'read'){
      var i = 0;
      while(i < this.state.contents.length){
        var data = this.state.contents[i];
        if(data.id === this.state.selected_content_id){
          _title = data.title;
          _desc = data.desc;
          break;
        }
        i = i+1;
      }
    }
</pre>
이 부분이고,  
  
ReadContent가 있던 부분을 변수처리한다.
<pre>
        < Control onChangeMode={function(_mode){
          this.setState({
            mode:_mode
          })
        }.bind(this)}>< /Control>
        {_article}
</pre>

그리고 _article이라는 변수를 선언하고 ReadContent 컴포넌트를 넣는다.  
mode가 read일때도 _article이 나와야 하기 때문에 아래에도 컴포넌트를 넣어준다.  
(위에는 mode가 welcome일 때 출력되는 article 이고 아래는 html, css, javascript 눌렀을 때 나타나는 article)  

<pre>
if(this.state.mode === 'welcome'){
      _title = this.state.welcome.title;
      _desc = this.state.welcome.desc;
      _article = < ReadContent title={_title} desc={_desc}>< /ReadContent>
    }else if(this.state.mode === 'read'){
      var i = 0;
      while(i < this.state.contents.length){
        var data = this.state.contents[i];
        if(data.id === this.state.selected_content_id){
          _title = data.title;
          _desc = data.desc;
          break;
        }
        i = i+1;
      }
      _article = < ReadContent title={_title} desc={_desc}>< /ReadContent>
    }

</pre>
<br>

그리고 mode가 create일 때는 CreateContent 컴포넌트가 화면에 출력되도록 해야 한다.  
else if 로 잇는다.

<pre>
//if문 


 if(this.state.mode === 'welcome'){
      _title = this.state.welcome.title;
      _desc = this.state.welcome.desc;
      _article = < ReadContent title={_title} desc={_desc}>< /ReadContent>
    }else if(this.state.mode === 'read'){
      var i = 0;
      while(i < this.state.contents.length){
        var data = this.state.contents[i];
        if(data.id === this.state.selected_content_id){
          _title = data.title;
          _desc = data.desc;
          break;
        }
        i = i+1;
      }
      _article = < ReadContent title={_title} desc={_desc}>< /ReadContent>
    }else if(this.state.mode === 'create'){
      _article = < CreateContent>< /CreateContent>

    }
</pre>

로 {_article}에 컴포넌트들을 넣어주면 된다.  
이렇게 하면 create를 클릭했을 때 Create 컴포넌트가 나타나게 된다.  

<br>