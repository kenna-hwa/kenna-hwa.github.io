---
layout: post
title:  "[React] React - Create 기능구현"
author: Kenna
date:   2021-07-16 21:26:35 +0830
image: https://images.unsplash.com/photo-1593720219276-0b1eacd0aef4?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1343&q=80
rating: 39
description: 인프런 - 생활코딩 React 수업
categories : React
tags: React
---

###### React
[Inflearn 생활코딩]("https://www.inflearn.com/course/react-%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9/dashboard")


###### create 구현 : form

글을 추가하는 기능의 폼 완성  
폼을 만들기 전 App.js의 mode를 Create로 바꾼다.-> 디버깅 편하게   

<br>

<pre>
      < form>
      < p>< input type="text" name="title" placeholder="title">< /input>< /p>
      < p>< textarea name="desc" placeholder="description">< /textarea>< /p>
      < p>< input type="submit">< /input>< /p>
      < /form>
</pre>

<br>

form에 action 같은 정보 전송 방식을 넣어주고 onSubmit 이벤트 함수를 넣는다.  
여기서 e.preventDefault(); 는 원래 submit 버튼을 누르면 action으로 지정된 곳으로 이동하게 되는데  
그 액션을 없애고 비동기적으로 페이지를 불러오게 된다. (바뀌는게 아니라 변경된다.)   

<pre>
      < form action="/create_process" method="post" 
      onSubmit={function(e){
        e.preventDefault();
        alert('submit!!!');
      }.bind(this)}
      >

      //폼은 이렇게
</pre>

<br>
이렇게 하면 경고창이 뜨지만 페이지 전환이 안된다!


다음은 app 컴포넌트 컨텐츠 끝에 사용자가 입력한 정보를 추가시키고  
글 목록도 자동으로 바뀌도록 해야한다.  


###### create 구현 : onSubmit 이벤트

submit을 사용자가 클릭했을 때 onSubmit 이벤트가 실행된다.   
이때 CreateContent 컴포넌트를 쓰고 있는 App 컴포넌트의 contents 데이터에 데이터를 하나 더 추가하는 방법을 알아보다.  

<br>

submit 클릭하면 CreateContent로 설치된 함수를 실행한다.  
인자로 title과 desc가 전달될 수 있다면  
setState를 통해서 새로운 content 값을 추가  
그러기 위해서 CreateContent의 onSubmit이라고 하는 props를 호출해야한다. 
<Br>

CreateContents.js 컴포넌트 파일 안에서  
props를 호출한다.


<br>
debugger; 로 이벤트 찾기  
onsumbit 이벤트 가 발생했을 때 form의 각각의 value값을 어떻게 가져올 수 있을까?  
<Br>

e의 target 자체가 form을 가리킨다.  
e - target 를 개발자도구로 보면 아-주 아래에 value가 이 form 값을 가져오는 것 볼 수 있다.  
그래서 이 title과 desc의 값은  
<br>

**e.target.title.value**<br>
**e.target.desc.value**<br>
로 가져올 수 있다.  

<br>
이런 사실을 바탕으로 위의 두개를 onsubmit의 인자로 준다.

<Br>

<pre>
     < form action="/create_process" method="post" 
      onSubmit={function(e){
        e.preventDefault();

        this.props.onSubmit(
          e.target.title.value,
          e.target.desc.value
          );

      }.bind(this)}
      >
</pre>
<br>

이렇게 되면 title과 desc 값을 얻을 수 있다!!



###### create 구현 : contents 변경

onsubmit이 발생했을 떄 CreateContent 컴포넌트의 onsubmit의 props가 실행되고 있다.  
App 컴포넌트에 contents 끝에 데이터가 추가되도록 하자.  

<br>

우선 id 값을 1 더 크게 만들어야 한다.
<pre>
      contents:[
        {id: 1, title: 'HTML', desc: 'HTML is information...'},
        {id: 2, title: 'CSS', desc: 'CSS is design...'},
        {id: 3, title: 'Javascript', desc: 'Javascript is interactive...'}
      ]
</pre>
<br>

<pre>
class App extends Component {
  constructor(props){
    super(props);
    this.max_content_id = 3;
    this.state = {
      mode: 'create', 
      selected_content_id: 2 , //기본적으로 2번 컨텐트가 선택
      subject:{title:'WEB', sub: 'world wide web!'},
      welcome:{title:'welcome', desc: 'Hello, React'},
      contents:[
        {id: 1, title: 'HTML', desc: 'HTML is information...'},
        {id: 2, title: 'CSS', desc: 'CSS is design...'},
        {id: 3, title: 'Javascript', desc: 'Javascript is interactive...'}
      ]
    }
  }
</pre>

App 컴포넌트 안에 객체의 값으로 별도 분리한 이유는
max_content_id는 데이터를 push 할 때 id 값을 뭐로 할까 하는 정보일 뿐  
ui에 영항을 주지 않기 때문에  
**state의 값이 되지 않는다.(안에 넣으면 불필요한 렌더링이 발생)**
<br>

그럼 이제 onSubmit 함수에 위의 값을 넣고 1 증가시킨다.
<pre>
this.max_content_id = this.max_content_id+1;
</pre>

<br>
그러면
<pre>
 {id:this.max_content_id, title:_title, desc:_desc}
</pre>

아래와 같은 객체를 생성해서 contents 끝에 추가한다.  
**setState**를 써서 변경한다!!   
<br>

배열에 값을 추가하는 방법은 두 가지
<br>

1) .push  
var arr = [1, 2];  
arr.push(3);  
arr = [1, 2, 3];  

<br>

**push는 원본을 바꾼다.**  <br>

2) .concat  
var arr2 = [1, 2];  
arr2.concat(3);  
arr2 = [1, 2, 3]  

**concat은 원본을 바꾸지 않는다.**<br>
새로운 배열을 변수에 담아 새 배열을 사용해야 한다.  

<br>

**리액트 state에 값을 추가할 때는 push와 같이 origin data를 건드는 것은 써선 안된다.**
**새로운 데이터를 추가하는 것을 써야한다.**<Br>

만약 지금의 경우   

<pre>
this.state.contents.push(  
{id:this.max_content_id, title:_title, desc:_desc}  
);    
</pre>
처럼 push 를 사용하면 기존 컨텐츠 배열에 값을 하나 추가하는 것  
push를 사용하는 방식은 추후 성능을 개선하기 어렵게 만들기 때문에  

<pre>
        var _contents = this.state.contents.concat(
          {id:this.max_content_id, title:_title, desc:_desc}
        )
        this.setState({
          contents: _contents
        });
</pre>
<br>
과 같이 이용해야 한다.  
이 방식은 어떻게 원본 데이터를 바꾸지 않으면서 데이터를 state에 갱신할 것인가 하는 것이다.  

<br>
