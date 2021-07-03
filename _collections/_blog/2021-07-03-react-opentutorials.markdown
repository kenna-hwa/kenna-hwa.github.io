---
layout: post
title:  "[React] React - state"
author: Kenna
date:   2021-07-03 11:26:35 +0830
image: https://images.unsplash.com/photo-1593720219276-0b1eacd0aef4?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1343&q=80
rating: 34
description: 인프런 - 생활코딩 React 수업
categories : React
tags: React
---

###### React
[Inflearn 생활코딩]("https://www.inflearn.com/course/react-%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9/dashboard")


###### State 소개
  
state는 props와의 차이점을 통해서 알 수 있다.   
어떠한 제품에 대한 사용자의 입장과 구현자에 대한 입장이 있다.   
사용자는 버튼이나 화면으로 기기를 조작(UI) 한다.   
props는 사용자가 조작하는 장치이다.   
  
<br>

그럼 구현자는 내부적인 구현을 위해 내부적 조작 장치를 가지고 있는데, 이것들이 state이다.  
  
<br>

props는 사용자가 컴포넌트를 사용하는데 있어 중요한 것이고,  
state는 props의 값에 따라 내부 구현에 필요한 데이터다.   
 
컴포넌트의 기본적인 동작을 바꾸려고 사용자에게 제공하는 것이  
tag에서는 attr에 해당하는 props다.  
<br>

< Component **props_name="props_value"**> < /Component>  
  

즉, **props는 component사용자에게 중요한 정보**이다.  
<br>
  

사용자가 몰라도 되는 컴포넌트 내부에서 사용되는 것을 **state**라고 한다.   
  
<br>

컴포넌트가 좋은 부품이 되기 위해서는   
컴포넌트를 사용하는 외부의 props와  
props에 따라 컴포넌트를 실제로 구현하는 내부의 state 정보가 철저히 분리되어야 한다.  
<br>

![state와 props]("https://github.com/kenna-hwa/kenna-hwa.github.io/blob/master/assets/images/blog/react/react.jpg?raw=true")

<br>

**사용자와 구현자의 기능을 철저하기 분리시켜 양쪽의 편의성을 도모하는 것!**
<br>

###### State 사용
  
현재  
<pre>
class App extends Component {
  render() {
    return (
      < div className="App">
        < Subject title="Web" sub="world wide web!">< /Subject>
        < TOC>< /TOC>
        < Content title="HTML" desc="HTML is Hypertext Markup Language.">< /Content>
      < /div>
    );
  }
}
</pre>
  
<br>
    
처럼 상위 컴포넌트 안에 하위 컴포넌트가 있고 하위 컴포넌트 안에 props가 하드코딩 되어 있다.  
이것을 state로 만들고 state의 값을 컴포넌트에 props로 전달하는 방법을 써보자.  
<br>
  
  
<pre>
//state값 초기화 하는 코드

  constructor(props){
    super(props);
    this.state={}
  }

</pre>
<br>
  
어떤 컴포넌트가 실행될 때 render() 함수보다 먼저 실행되면서 **컴포넌트를 초기화 시키는 코드**는 constructor를 위와 같이 짜고 안에 코드를 작성한다.  
  
<br>

<pre>
//코드 작성

  constructor(props){
    super(props);
    this.state = {
      subject: {title: 'WEB', sub: "world wide web!"}
    }
  }
</pre>
<br>

    
이렇게 subject에 객체를 만들어주고  
이 객체를 사용하기 위해서는 아래와 같이 App 컴포넌트를 바꿔준다.  
  
<br>


<pre>
// "" 따옴표를 {} 중괄호로 바꿔서 자바스크립트 코드로 실행되게 객체를 가지고 온다.
// 여기서의 WEB은 위 constructor 에서 가지고 온 정보다.  

class App extends Component {
  render() {
    return (
      < div className="App">
        < Subject title={this.state.subject.title} sub="world wide web!">< /Subject>
        < TOC>< /TOC>
        < Content title="HTML" desc="HTML is Hypertext Markup Language.">< /Content>
      < /div>
    );
  }
}
</pre>
  
<br>

App.js를 사용하고 있는 파일은 index.js다.  
index.js에는 현재 이런 코드로 App 컴포넌트를 불러오고 있다.  
<br>

<pre>
ReactDOM.render(
    < App />, document.getElementById('root')
);
</pre>
<br>
  
지금 우리는 이 코드에서 내부적으로 State값이 Subject 값이 있는지 없는지 모른다.  
외부에서 알 필요가 없는 기능을 철저하게 숨기는 것이  
**좋은 사용성**을 만드는 핵심이다.  

<br>

![내부 부품이 다 보일 필요는 없다.]("https://github.com/kenna-hwa/kenna-hwa.github.io/blob/master/assets/images/blog/react/brokenphone.jpg?raw=true")
<br>

App이 내부적으로 사용하는 상태는 state를 사용한다.  
이 state값을 subject 컴포넌트의 props의 값으로 줬다.
  
**상위 컴포넌트의 상태를 하위 컴포넌트로 전달하려고 할 때는 상위 컴포넌트의 state 값을 하위 컴포넌트의 props의 값으로 전달한다.**

<br>

###### key

이전의 state는 subject 프로퍼티의 값 하나였는데  
여러 개를 사용할 때는 방법이 달라진다.  
<br>

지금 만든 글 목록 TOC 컴포넌트 안의 데이터를 App의 내부 state를 TOC에 주입하여 자동으로 값이 바뀌도록 해본다.
TOC는 값이 많으니까 **배열**을 사용한다.  
<br>
  
<pre>
constructor(props){
    super(props);
    this.state = {
      subject:{title:'WEB', sub: 'world wide web!'},
      contents:[
        {id: 1, title: 'HTML', desc: 'HTML is information...'},
        {id: 2, title: 'CSS', desc: 'CSS is design...'},
        {id: 3, title: 'Javascript', desc: 'Javascript is interactive...'}
      ]
    }
  }
</pre>
<br>

이 contents에 담겨 있는 배열을 TOC 컴포넌트에 넣어준다.  
원래 TOC는 props가 없었기 떄문에 data props를 만들어서 배열을 불러온다.  
  
<br>

<pre>
class App extends Component {
  render() {
    return (
      < div className="App">
        < Subject title={this.state.subject.title} sub="world wide web!">< /Subject>
        < TOC data={this.state.contents}>< /TOC>
        < Content title="HTML" desc="HTML is Hypertext Markup Language.">< /Content>
      < /div>
    );
  }
}
</pre>
<br>

이렇게 되면 불러온 TOC 컴포넌트는 this의 props의 data라는 값을 가지고 있다.  
`this.props.data`  
  
<br>

이때 반복문을 쓴다.  
변수 i를 선언해서 값 0 을 할당한다.  
`this.props.data`를 변수 data에 할당한다.  
아래 메뉴를 형성하는 ul의 li를 배열에 담기 위해 lists라는 변수를 선언하고 빈 배열을 만든다.  
<br>
  
<pre>
var data = this.props.data;
var i = 0;
var lists = [];
</pre>
<br>
  
while문 안에 i가 data의 갯수만큼 반복하도록 하고  
반복할 때마다, 빈 배열을 할당한 변수 lists 안에 li 태그가 하나씩 들어가도록 한다.  
<br>
  
<pre>
      while(i< data.length){
        lists.push(< li>< a href={" /contents /"+data[i].id}>{data[i].title}< /a>< /li>);
        i = i+1;
      }
</pre>
<br>
  

여기서 data[ i].는 인덱스로 lists 배열에서 0, 1, 2번째 인덱스를 선택하는 것이고,  
a href=""안의 id 값은 this.state의 contents의 id 값이다.
중괄호 안의 data[ i]는 숫자 1. 2. 3.이고, title은 this.state의 contents의 title 값이다.   
<br>
   
그럼 그 배열 lists를 아래 return값 안의 ul>li를 지우고 대체한다.  
  
<br>
  
<pre>
class TOC extends Component {
    render() {
      var lists = [];
      var data = this.props.data;
      var i = 0;
      while(i< data.length){
        lists.push(< li>< a href={"/contents/"+data[i].id}>{data[i].title}< /a>< /li>);
        i = i+1;
      }
      return(
        < nav>
        < ul>
            {lists}
        < /ul>
        < /nav>
      );
    }
  }
</pre>
<br>
  
이렇게 하면 App.js 에서 contents만 만지면 TOC는 열 필요가 없다.
지금은 lists.push를 통해서 li 엘리먼트를 여러 개 생성하고 있다.  
엘리먼트를 자동으로 생성하게 되면 console에 에러가 발생할 수 있다. 
`index.js:1 Warning: Each child in a list should have a unique "key" prop.`  
: 각각의 list의 항목들은 key라는 props를 가지고 있어야 한다.  
여기서 key는 **'식별자'**이다.  

<br>
  
그래서 lists.push를 바꿔준다.   
<br>

<pre>
//li에 리액트가 필요로 하는 식별자를 넣어준다.

lists.push(< li key={data[i].id}>< a href={"/contents/"+data[i].id}>{data[i].title}< /a>< /li>);
</pre>
<br>

부모인 App.js 입장에서는 state라고 하는 내부정보를 사용했고  
이것을 자식(하위 컴포넌트)에게 전달할 때는 props라는 것을 통해 전달하고 있다.  
App.js의 입장에서는 data로로 어떤 정보를 전달하면 되는가 하는 사용자의 입장에서 알아야 할 것만 알면 된다.  


<br>
