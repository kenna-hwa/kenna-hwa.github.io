---
layout: post
title:  "[React] React - Create 기능구현"
author: Kenna
date:   2021-07-16 21:26:35 +0830
image: https://images.unsplash.com/photo-1593720219276-0b1eacd0aef4?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1343&q=80
rating: 41
description: 인프런 - 생활코딩 React 수업
categories : React
tags: React
---

###### React
[Inflearn 생활코딩]("https://www.inflearn.com/course/react-%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9/dashboard")


###### update 구현 : Update 구현

update는 read와 create 기능이 결합된 것으로 볼 수 있다.   
폼이 있어야 수정할 수 있고 기존 컨텐츠를 불러와야 한다.  

<br>

그래서 form이 이미 구현된 createContent.js 컴포넌트를 복사해준다.  

CreateContent 를 UpdateContent로 바꿔주고 App.js에도 사용할 수 있도록 넣어준다.

<br>

<pre>
import UpdateContent from './components/UpdateContent';
</pre>

그리고 mode 가 update가 되면 실행되도록 if .. if else문의 if else를 복사해서 하나 더 만들어준다.  

<br>

지금 render 부분이 너무 혼란스럽기 때문에 새로운 함수를 만들어 쪼갠다. 

<pre>
 getContent(){
    var _title, _desc, _article = null;
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
      _article = < CreateContent onSubmit={function(_title, _desc){
        //인자로 title과 desc가 전달될 수 있다면
        //setState를 통해서 새로운 content 값을 추가
        //this.state.contents

        //id 값 1 증가시키기
        this.max_content_id = this.max_content_id+1;
        // this.state.contents.push(
        // {id:this.max_content_id, title:_title, desc:_desc}
        // ); 기존 컨텐츠 배열에 값을 하나 추가하는 것

        // var _contents = this.state.contents.concat(
        //   {id:this.max_content_id, title:_title, desc:_desc}
        // )

        //Array.from 쓰기
        var newContents = Array.from(this.state.contents);
        newContents.push({id:this.max_content_id, title:_title, desc:_desc});
        this.setState({
          contents: newContents
        });

        //this.setState({
        //  contents: _contents
        //});
      }.bind(this)}>< /CreateContent>
    }else if(this.state.mode === 'update'){
      _article = < UpdateContent onSubmit={function(_title, _desc){
        this.max_content_id = this.max_content_id+1;
        var newContents = Array.from(this.state.contents);
        newContents.push({id:this.max_content_id, title:_title, desc:_desc});
        this.setState({
          contents: newContents
        });
      }.bind(this)}>< /UpdateContent>
    }
    return _article;
  }  
</pre>

그리고 아래 Control 컴포넌트에 `_article` 대신 `this.getContent()` 를 넣어준다.  

그 다음 UpdateContent가 실행될 때  
입력값으로 현재 선택된 content id에 따른 값을 UpdateContent에 넣어줘야 한다.  

contents에서 selected_content_id와 같은 원소를 찾아줘야 한다.  
read에서 썼던 것 처럼 while문으로 찾아준다.  
<br>

getContent() 위에 getReadContent()라는 새로운 함수를 만들고  
아래에서 사용한 변수를 넣어준다.

<pre>
  getReadContent(){
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
</pre>

그리고 _title과 _desc부분을 data 로 바꿔주고  

<pre>
  getReadContent(){
    var i = 0;
      while(i < this.state.contents.length){
        var data = this.state.contents[i];
        if(data.id === this.state.selected_content_id){
          return data;
          break;
        }
        i = i+1;
      }
</pre>

아래의 while문을 getReadContent();함수로 바꿔준다.  

<pre>
else if(this.state.mode === 'read'){
      var _content = this.getReadContent();
      _article = < ReadContent title={_content.title} desc={_content.desc}>< /ReadContent>
    }
</pre>

그리고 아까 만들어 둔 else if update 부분에도  
`_content = this.getReadContent();` 을 넣어준 후, UpdateContent에 data로 넣어준다.  

<pre>
else if(this.state.mode === 'update'){
      _content = this.getReadContent();
      _article = < UpdateContent data={_content} onSubmit={function(_title, _desc){
        this.max_content_id = this.max_content_id+1;
        var newContents = Array.from(this.state.contents);
        newContents.push({id:this.max_content_id, title:_title, desc:_desc});
        this.setState({
          contents: newContents
        });
      }.bind(this)}>< /UpdateContent>
    }
</pre>

그리고 UpdateContent에서 console로 찍어보면 console에 해당 데이터가 잘 들어오는 것을 알 수 있다.  


<br>



###### update 구현 : form

컴포넌트로 주입된 data를 기반으로 컴포넌트에 기본적으로 입력되는 값을 세팅하기  

<br>

반드시 참고해야 하는   
[React.js]("https://ko.reactjs.org/docs/forms.html")  


<br>
UpdateContent.js 파일의 input 부분을 이렇게 줄바꿈 한다.  

<pre>
  < p>
  < input 
    type="text" 
    name="title" 
    placeholder="title"
    ></>
  < /p>
  < p>
    < textarea 
    name="desc" 
    placeholder="description"
    >< /textarea>
  < /p>
  < p>
    < input 
    type="submit"
    >< /input>
  < /p>
</pre>

그리고 input title 부분에 `value={this.props.data.title}`를 넣어주면  
다시 새로고침 했을 때 title 부분에 지금 지정된 id 값의 title이 들어온다.  
그러나 수정은 안된다.   
왜냐면 `this.props.data.title`에서 가지고 온 데이터는 props에서 가지고 온 것이기 때문에   
수정할 수 없는 readonly 상태가 된다.  

<br>

그러면 컴포넌트 내에서 value에 넣을 값을 **state화** 시켜준다.   

<pre>
  constructor(props){
    super(props);
    this.state = {
      title:this.props.data.title
    }
  }
</pre>

props 를 생성자로 생성하고   
이제 `this.props.data.title`의 this.props.data를 this.state로 바꿔준다.   

<br>

하지만 아직 props가 state가 되었다고 해서 수정이 가능해질 근거가 없다.   
input의 값을 바꾸었을 때 state의 값이 바뀌어야만 readonly가 풀린 것으로 본다.  
그러면 input에 onChange 이벤트를 넣어준다.

<br>

<pre>
      < p>
        < input 
        type="text" 
        name="title" 
        placeholder="title"
        value={this.state.title}
        onChange={function(e){
          console.log(e.target.value);
        }.bind(this)}
        >< /input>
      < /p>
</pre>

이렇게 되면 한 글자씩 변할때마다 콘솔에 출력된다.  
이제 여기에 `this.setState({title:e.target.value});` 를 넣어 주면 수정이 된다.  

<br>

< pre>
 <p>
    < input 
    type="text" 
    name="title" 
    placeholder="title"
    value={this.state.title}
    onChange={function(e){
      console.log(e.target.value);
      this.setState({title:e.target.value});
    }.bind(this)}
    >< /input>
    < /p>
</pre>

<br>

그럼 이제 textarea도 setState를 넣어줘야 한다.  
props에 title을 만들어 두었던 곳 아래에 desc도 만들어 준다.  

<pre>
  constructor(props){
    super(props);
    this.state = {
      title:this.props.data.title,
      desc:this.props.data.desc
    }
  }
</pre>  

그리고 textarea도 다음과 같이 바꾸고 onChange이벤트도 그대로 가지고 와서 title을 desc로 바꾼다.  

<pre>
 < p>
  < textarea 
    onChange={function(e){
          console.log(e.target.value);
          this.setState({desc:e.target.value});
        }.bind(this)}
        name="desc" 
        placeholder="description"
        value={this.state.desc}
  > < /textarea>
  < /p> 
</pre>

<br>

하지만 이렇가 하나하나 onChange를 만드는 것은 귀찮기 때문에  
inputFormHandler(){}라는 이름의 함수를 하나 만들어서 중복을 제거한다.  

<pre>
  inputFormHandler(e){
    this.setState({title:e.target.value});
  }
</pre>

그리고 input의 onChange를 바꾼다.  

<pre>
< p>
  < input 
  type="text" 
  name="title" 
  placeholder="title"
  value={this.state.title}
  onChange={this.inputFormHandler.bind(this)}
  >< /input>
< /p>
</pre>


<br>

하지만 이 경우에는 setState에 title이라고 되어 있기 때문에  
아래 desc 에서는 사용할 수 없으므로  
지금 이벤트가 발생하고 있는 태그의 name을 알아내는 방법을 쓴다.  
title을 지우고 `e.target.name`을 사용해 다음과 같이 만든다.  

<pre>
  inputFormHandler(e){
    this.setState({[e.target.name]:e.target.value});
    //대괄호 사용
  }
</pre>

이렇게 하면 title 부분에 target의 name이 대신 들어오게 된다.  

그리고 construnctor에다가 bind(this)를 가지고 있을 수 있게 만든다.  

<pre>
  constructor(props){
    super(props);
    this.state = {
      title:this.props.data.title,
      desc:this.props.data.desc
    }
    this.inputFormHandler = this.inputFormHandler.bind(this);
  }
</pre>
  
그러면 이제 아래에 일일이 bind(this)를 가지고 있을 필요가 없다.  

<br>


###### update 구현 : state 변경

이전시간까지 props로 들어온 데이터를 state로 만들고 state의 값을 각각의 폼과 동기화 시키는 방법을 구현했다.  
하지만 어디에 대한 부분을 업데이트 할 것인지 식별자 부분이 필요하다.  

폼에서는 사용자에게 보일 필요가 없는 부분에 hidden을 쓴다.  

<pre>
< input type="hidden" name="id" value={this.state.id}>< /input>
</pre>

form 안에 hidden을 넣어준다.  
변경이 없기 때문에 onChange 는 들어갈 필요 없다.  

그리고 onSubmit 이벤트 발생 시 id 값을 넣어준다.  

<pre>
< form action="/create_process" method="post" 
      onSubmit={function(e){
        e.preventDefault();
        this.props.onSubmit(
          this.state.id,
          this.state.title,
          this.state.desc
          );
      }.bind(this)}
      >
</pre>

그리고 App.js의 Update 부분을 수정한다.  

onSubmit이 실행될 때 첫번째 인자로 id값을 주는 것으로 바꾼다.
<br>

<pre>
else if(this.state.mode === 'update'){
      _content = this.getReadContent();
      _article = < UpdateContent data={_content} onSubmit={
        function(_id, _title, _desc){
        this.max_content_id = this.max_content_id+1;
        var _contents = this.state.contents.concat(
          {id:this.max_content_id, title:_title, desc:_desc}
          );
        this.setState({
          contents: _contents
        });
      }.bind(this)}>< /UpdateContent>
    }
</pre>

그리고 max_content_id는 create를 할 때 필요한 것이기 때문에 삭제한다.  
concat은 기존 데이터를 추가할 때 썼던 것인데 지금은 수정하려고 한다.
그러기 위해 변수 _contents를 복제한다.  

<br>

**Array.from**를 사용한다.  

<br>

`Array.from(this.state.contents);` 하면 this.state의 contents 배열이 복사되어 새로 만들어진다.  


이것을 _contents라는 변수에 담아준다. 
그 다음이 _contents에 담긴 값 중에서 우리가 수정해야 하는 값을 찾는다.  

<pre>
  var i = 0;
    while(i < contents.length){
      if(_contents[i].id === _id){
        _contents[i] = {id:_id, title:_title, desc:_desc}
        break;
      }
    i = i + 1;
  }
</pre>

<br>

기존 원본을 수정하지 않고 immutable 테크닉으로 기존의 것을 복제해서 사용해야 한다.  

<br>

수정 후 바로 내용을 보기 위해 mode를 read로 바꿔준다.  

<br>

###### update 구현 : delete 구현

mode를 welcome으로 바꿔둔다.  
<br>

delete 버튼은 Control 컴포넌트 안에 있다.  
delete 는 onChangeMode라는 props를 호출하고 있다.    
_mode 라는 값이 delete로 호출되면 삭제 오퍼레이션이 시작된 것이다.  

App.js의 Control 부분에 조건문으로 mode가 delete인 경우 삭제 오퍼레이션을 진행할 수 있게  
조건문을 넣어준다.  

<pre>
   < Control onChangeMode={function(_mode){
          if(_mode === 'delete'){
            //정말 삭제?
            if(window.confirm()){
              

            }
          } else{
            this.setState({
              mode:_mode
            })
          }
        }.bind(this)}>< /Control>
</pre>


`window.confirm()` 은 `alert()` 와 다르게 window가 붙어야 한다.  

이 confirm을 실행했을 때, 사용자가 확인을 누르면 delete가 실행되도록 한다. 
누구를 삭제할 것인가는 State의 selected_content_id를 통해 알 수 있다.  
어떤..데이터...?(잘 안들리는 2:53) 를 삭제할 것인가는 contents라고 되어있는 부분에서 찾아야 한다.  

<br>

while 문을 사용한다.  

이 떄 삭제는 **splice()** 를 사용한다.  


<pre>
  < Control onChangeMode={function(_mode){
    if(_mode === 'delete'){
      //정말 삭제?
      if(window.confirm('really??')){
        var _contents = Array.from(this.state.contents);
        var i = 0;
        while(i < _contents.length){
          if(_contents[i].id === this.state.selected_content_id){
            _contents.splice(i, 1);
            break;
          }
          i = i + 1;
        }
        this.setState({
          mode:'welcome',
          contents:_contents
        });
        alert('deleted!');
      }
    } else{
      this.setState({
        mode:_mode
      })
    }
  }.bind(this)}>< /Control>
</pre>

이럼 삭제 완료!  

<br>

###### 수업을 마치며

**immutable 라이브러리**  <br>

배열, 객체의 대체재로 사용할 수 있다.  
복제된 원본이 수정된 결과를 리턴한다.  

<br>
리액트와 단짝이다.  

<br>

**react router**
<br>


url에 따라 적당한 컴포넌트를 사용할 수 있도록 한다.  
플러그인과 같은 기능으로 permalink 기능도 제공한다.  

**create-reate-app**을 확장하려면
**npm run eject**을 하면 사용이 가능하다. 

<br>

**redux**

부모 자식간 이벤트를 이동시킬 때 사용한다.   
중앙에 데이터 저장소를 만들고 모든 컴포넌트는 중앙 저장소와 직접 연결되어 저장소의 데이터가 변경될 때  
연결된 모든 데이터를 수정해준다.  

<br>

**react server side rendering** <br>
서버사이드에서 페이지를 완성하고 클라이언트 단으로 보낸다.  
자바스크립트 특유의 로딩이 필요없는 애플리케이션 같은 특성을 유지할 수 있다.  

검색 로봇 등에게 친화적인 기술이다.
<br>

**react native**
하나의 코드로 모든 플랫폼에서 동작하는 앱을 만들 수 있다.  

<br>