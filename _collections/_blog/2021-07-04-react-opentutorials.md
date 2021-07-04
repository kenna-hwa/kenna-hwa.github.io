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


###### 이벤트에서 state 변경하기

state와 event 작업을 연결한다.  
a 태그를 클릭했을 때 App 이라고 하는 컴포넌트의 mode 를 'welcome'으로 바꾸려고 한다.
<br>

`e.preventDefault();` 아래에  
`this.state.mode = 'welcome';`을 넣어본다.   
이 값은 두 가지의 문제를 가지고 있기 때문에 오류가 뜬다.       
   

이 onClick 되었을 때 호출되는 함수는 this의 값이 아무 값도 셋팅되어 있지 않았다.  
그래서 state를 읽을 수 없다고 나온다.  
그래서 앞으로 이벤트를 설정할 때, this가 정의되지 않았다고 하면   
함수가 끝난 직후에 bind(this)를 넣어준다.   
<br>
그러면 this는 우리의 컴포넌트가 된다.
<br>

<pre>
<header> 
//Subject.js

    < h1>< a href="/" onClick={function(e){
      console.log(e);
      e.preventDefault();
      this.state.mode = 'welcome';
      }.bind(this)}>{this.state.subject.title}< /a>< /h1>
    {this.state.subject.sub}
< /header>
</pre>
  
하지만 이렇게 짜면 state의 값이 바뀐 것을 리액트는 모른다.  
그래서 `this.state.mode = 'welcome';`이 아닌   
`this.steState({mode:'welcome'})'`을 넣어준다.  
<br>
<pre>
<header> 
//Subject.js

    < h1>< a href="/" onClick={function(e){
      e.preventDefault();
      this.setState({
              mode:'welcome'
            });
      }.bind(this)}>{this.state.subject.title}< /a>< /h1>
    {this.state.subject.sub}
< /header>
</pre>
  
<Br>

이러면 WEB을 눌렀을 때 welcome과 Hello, React가 나타나게 된다.

<br>

###### 이벤트 bind 함수 이해하기

`bind();`
<br>
묶어주는 함수  
render()가 호출될 때의 this는 render() 함수가 속해 있는 App 컴포넌트 자신 스스로를 가리킨다.  
  
onClick에서 실항하는 function에는 this값이 정의되지 않았다.  
그래서 this를 bind 시켜주면 이 function에서 사용할 수 있게 되는 것.   
<br>
bind로 인해서 괄호 안의 객체를 참조한다.  
그래서 bind(this)하면 this는 App이라고 하는 컴포넌트 자체를 가리키는 객체를 function(e)안으로 주입해서 그 객체가 되도록 한다.  

<br>

###### 이벤트 setState 함수 이해하기

`this.setState();` 함수를 통해 함수의 값을 변경해야 하는 이유  
constructor()라는 생성자 함수에서는 this.state에서 수정하면 된다.  
그러나 이미 컴포넌트가 생성된 이후에 동적으로 state의 값을 수정하기 위해서는  
setState() 함수를 사용해야 한다.    
(`this.state.mode = 'welcome` 처럼 해서는 안된다.)  

<br>

`this.setState()` 함수에 값을 객체 형태로 주는 것을 통해 수정해야 한다.  
<br>

리액트 입장에서는 `this.state.mode`처럼 바꾸면 바꿨는지 알 수가 없다.   
그래서 렌더링 해주지 않는다.  

함수가 내부적으로 일하면서 state의 내용을 바꿔주는 것.  
state 값은 **setState()**로 바꿔줘야 한다!  

<br>

###### 컴포넌트 이벤트 만들기 1

이벤트를 만들어서 태그나 컴포넌트를 사용하는 사람들이 이벤트를 사용할 수 있도록 생산자가 되어본다.  
<br>

Subject 컴포넌트를 사용하는 사용자가 a 링크를 클릭했을 때  
발생할 이벤트를 설치하고 싶다면  
**onChange** 이벤트를 사용한다.  
이 이벤트에 함수를 설치해두면 클릭할 때 설치한 이벤트의 함수를 실행한다.  
<br>
<pre>
//App.js

  < Subject 
    title={this.state.subject.title} 
    sub={this.state.subject.sub}
    onChangePage={function(){
      alert('hihihi');
    }.bind(this)}
    >
  < /Subject>
</pre>
<br>

이 `onChangePage`라고 하는 이 함수는 props 형태로 Subject 컴포넌트에 전달된다.  
그래서 Subject.js에서는 `onClick` 함수를 추가한다.   
이 `onClick` 함수는 클릭할 때 실행되는 이벤트를 추가하면 되고,  
props로 전달 된 onChangePage의 함수를 넣어준다.
<br>

<pre>
//Subject.js

class Subject extends Component {
    render() {
      return(
      < header>
          < h1>< a href="/" onClick={function(e){
            e.preventDefault();
            this.props.onChangePage();
          }.bind(this)}>{this.props.title}< /a>< /h1>
          {this.props.sub}
        < /header>
      );
    }
  }

  export default Subject;
</pre>
<Br>
Subject 컴포넌트에 onChangePage라고 하는 이벤트를 만들었다. 


<br>

###### 컴포넌트 이벤트 만들기 2


지금까지 Subject 컴포넌트에 onChangePage 함수를 만들어 사용자에게 이벤트를 제공했다.
   
이번에는 글 목록을 클릭했을 때 App 컴포넌트의 state의 mode를 read 로 바꾸고 contents 라는 state가 본문에 나오게 하자.  
  
글 목록은 TOC 컴포넌트로 TOC에 onChangePage 함수를 넣는다.  

<br>

<pre>
//App.js

< TOC onChangePage={function(){
          alert('hi');
        }.bind(this)} 
        data={this.state.contents}>< /TOC>
</pre>
<br>

그리고 TOC 컴포넌트에 onClick 함수를 넣는다.   
onClick 함수에는 `e.preventDefault();`를 넣어준다.   
`this.setState({mode : 'read'});`로 state를 바꿔준다.  

<pre>
</pre>
//App.js

< TOC onChangePage={function(){
          this.setState({mode: 'read'});
        }.bind(this)} 
        data={this.state.contents}>< /TOC>

<br>

###### 컴포넌트 이벤트 만들기 3

글 목록에서 클릭한 메뉴에 맞는 contents가 화면에 표시되게 만들자.  
App의 state에 selected_content_id 같은 이름을 주어서 현재 활성화 된 컨텐트를 표시한다.  
<Br>
constructor 생성자 함수가 실행될 떄,
this.state에 selected_content_id를 주고 기본적으로 2가 선택되도록 한다.  
<br>
<pre>
  constructor(props){
    super(props);
    this.state = {
      mode: 'read', 
      selected_content_id:2, //기본적으로 2번 컨텐트가 선택

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

<br>

render()함수가 실행될 때 `this.state.mode`의 값이 read 일 때 state의 title과 desc를 받아오도록 조건문을 생성한다.  

<br>

<pre>
  render() {
    var _title, _desc = null;
    if(this.state.mode === 'welcome'){
      _title = this.state.welcome.title;
      _desc = this.state.welcome.desc;
    }else if(this.state.mode === 'read'){
      var i = 0;
      while(i < this.state.contents.length){
        var data = this.state.contents;
        if(data.id === this.state.contents.selected_content_id){
          _title = data.title;
          _desc = data.desc;
          break;
        }
        i = i+1;
      }
    }

    return (
      < div className="App">
        < Subject 
        title={this.state.subject.title} 
        sub={this.state.subject.sub}
        onChangePage={function(){
          this.setState({mode: 'welcome'});
        }.bind(this)}
        >
        < /Subject>
        < TOC onChangePage={function(){
          this.setState({mode: 'read'});
        }.bind(this)} 
        data={this.state.contents}>< /TOC>
        < Content title={_title} desc={_desc}></ Content>
      < /div>
    );

  }
</pre>
<br>

이러면 TOC.js에 있는 props를 실행시키는 것을 통해서 App.js의 onChangePage함수를 실행시키게 되는데 실행할 때의 인자로 클릭한 항목의 id값을 보내주면 된다.  
<br>

 `data-id = {data[i].id}`로 data-id라는 속성을 만들고 속성값을 준다.
<br>
이벤트 객체는 target이라는 속성을 가진다.  
target 속성은 이벤트가 발생한 태그(지금은 a)를 가리킨다.
그래서 e.target은 이벤트가 소재한 태그(지금은 a를) 가리키고 이것을 통해  
a 태그가 가진 id 값에 접속할 수 있다.  
<br>

`data-`로 시작하는 속성은 **dataset**이라고 하는 특수한 곳을 통해 알 수 있다.  
따라서 `e.target.dataset.id`로 id값을 알아낼 수 있다. 
이 `e.target.dataset.id`는 onChangePage 의 인자로 App.js의 onChangePage 함수로 넘어가게 되고,  
함수의 인자 값을 id라고 주었을 때
this.setState의 selected_content_id의 값을 넘어온 인자인 id 값으로 설정한다.  

<br>
<pre>
//TOC.js

render() {
    var lists = [];
    var data = this.props.data;
    var i = 0;
    while(i< data.length){
      lists.push(
      < li key={data[i].id}>
        < a 
        href={"/contents/"+data[i].id}
        data-id = {data[i].id}
        onClick={function(e){
          e.preventDefault();
          this.props.onChangePage(e.target.dataset.id);
        }.bind(this)}
        >{data[i].title}< /a>
      < /li>);
      i = i+1;
    }

//App.js
  < TOC onChangePage={function(id){
      this.setState({
        mode: 'read',
      selected_content_id:id
    });
    }.bind(this)} 
  data={this.state.contents}>< /TOC>
</pre>
<br>

이러면 id값이 문자로 들어오기 때문에 숫자로 변환하는 Number로 감싸주면 숫자가 된다.  

<br>
<pre>
    < TOC onChangePage={function(id){
        this.setState({
          mode: 'read',
        selected_content_id:Number(id);
      });
      }.bind(this)} 
    data={this.state.contents}>< /TOC>
</pre>

<br>
혹은  
bind에 두 번째 인자를 주면 묶여있는 함수에 매개변수의 값으로 전달하기 때문에  
기존 매개변수 e를 두 번째로 주고 id를 첫 번째 매개변수를 주어서 쓸 수도 있다.  

<br>

<pre>
render() {
      var lists = [];
      var data = this.props.data;
      var i = 0;
      while(i < data.length){
        lists.push(
        < li key={data[i].id}>
          < a 
          href={"/contents/"+data[i].id}
          onClick={function(id, e){
            e.preventDefault();
            this.props.onChangePage(e.target.dataset.id);
          }.bind(this, data[i].id)}
          >{data[i].title}< /a>
        < /li>);
        i = i+1;
      }
</pre>
<br>