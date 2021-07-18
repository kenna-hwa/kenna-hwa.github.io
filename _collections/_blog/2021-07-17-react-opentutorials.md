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


###### create 구현 : shouldComponentUpdate

push와 concat  

concat을 써라.  
setState에 값을 줄 때는 값을 수정할 때 (push를 통해 수정할 떄)  
원본의 복제본을 수정해서 복제본을 setState 값으로 주어라.  

<br>

글 목록 컴포넌트 TOC가 화면에 표시되기 위해 필요한 데이터는 
App.js의 contents의 배열들이다.  
배열 내용이 바뀌었다면 TOC컴포넌트의 render 메소드가 호출되면서 TOC가 다시 그려져야 한다.  

<br>
따라서 contents 배열이 바뀌지 않았다면 TOC컴포넌트의 render이 호출되지 않아도 된다. (재랜더링이 이루어지지 않아도 된다.)
새로 랜더링이 계속 된다는 것은 불합리한 상황일수도 있다.  
특히 큰 프로그램이 될 수록 중요한 이슈로 부상하게 된다.  

<br>

성능 향상을 위해 컴포넌트의 render 함수가 실행될지 안될지를 개발자가 결정할 수 있도록 특정 함수를 제공한다.  

<br>

**shouldComponentUpdate(){}**

<br>

<pre>
import React, { Component } from 'react';

class TOC extends Component {

  shouldComponentUpdate(){
    console.log('===> TOC shouldComponentUpdate');
    return true;
  }
    render() {
      console.log('===> TOC render');
      var lists = [];
      var data = this.props.data;
      var i = 0;
      while(i< data.length){
        lists.push(
        < li key={data[i].id}>
          < a 
          href={"/contents/"+data[i].id}
          data-id={data[i].id}
          onClick={function(e){
            e.preventDefault();
            this.props.onChangePage(e.target.dataset.id);
          }.bind(this)}
          >{data[i].title}< /a>
        < /li>);
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

  export default TOC;
  </pre>

  <Br>
  TOC에 console.log를 찍고 create를 눌러보면 바꿀 때 마다 shouldComponentUpdate가 호출 된 다음  
  render함수가 호출되고 있음을 알 수 있다.  

  TOC의 부모인 App.js의 state 값이 바뀌면 부모의 자식들은 모두 render 함수가 호출되었다. 
  그런데 shouldComponentUpdate를 false로 주게 되면 shouldComponentUpdate가 있는 해당 컴포넌트의 shouldComponentUpdate는 호출되고  
  render 함수는 호출되지 않는다.  

  <br>

  shouldComponentUpdate는 두 개의 매개변수를 갖는다.
  **shouldComponentUpdate(newProps, newState)** <Br>

  하나는 newProps 두번째는 newState로   
  TOC 컴포넌트의 props가 바뀌었을 때의 값이 newProps, newState는 state가 바뀌었을 때의 값이다.

  <pre>
    shouldComponentUpdate(newProps, newState){
    console.log('===> TOC shouldComponentUpdate'
    , newProps.data
    ,this.props.data
    );
    return false;
  </pre>

  이렇게 찍어서 TOC의 HTML을 클릭하면 찍히는 콘솔이 둘 다 같다.    
  그러면 이제 create에서 새로운 글을 입력 제출 해보면 `newProps`는 원소가 4개인 데이터고    
  이전 `this.props.data`는 원소가 3개인 데이터다.  
  <br>

  **즉, 첫 번째 인자를 통해 바뀐 값을 알 수 있고 두 번째 인자를 통해 현재 값을 알 수 있다.**

  <br>
  종합해보면,  
  render 이전에 shouldComponentUpdate 가 실행된다.  
  shouldComponentUpdate 리턴 값이 trun면 render가 호출된다. false면 render가 호출되지 않도록 약속되어 있다. 
  shouldComponentUpdate는 새 값과 이전 값에 접근할 수 있다.  
  <br>
  종합하면 TOC로 들어오는 data의 props의 값이 바뀌었을 때 render가 호출되고, 바뀌지 않았으면 render를 호출하지 않는 것이 좋다.

  <br>
  <pre>
    shouldComponentUpdate(newProps, newState){
    console.log('===> TOC shouldComponentUpdate'
    , newProps.data
    ,this.props.data
    );
    if(this.props.data === newProps.data){
      return false;
    }else{
      return true;
    }
  </pre>

  <br>
  이렇게 되면 새 글을 입력하지 않고 그냥 TOC를 입력하면 render가 호출되지 않고  
  새 글을 입력하면 render를 호출한다. (우와 우와!)
  <Br>

  만약 concat이 아니라 push로 구현을 하면 기존 `this.state.contents`의 원본을 바꾸기 때문에 추후 내용을 바꾸더라도 변화가 생기지 않는다.
  <Br>
  하지만 작은 프로그램이나 유지보수를 하지 않는다면 굳이 concat이나 push를 구분할 필요는 없다.  
  그리고 shouldComponentUpdate도 사용하지 않는다면 또 구분할 필요는 없다.   

###### create 구현 : immutable

  shouldComponentUpdate를 사용하는 경우  

  원본을 바꾸지 않는다 -> **불변성immutable**  

  <br>

  <pre>
  var a = [1, 2];  
  var b = Array.from(a);  
    
  a === b -> false  
  </pre>

  <br> 
  a와 b의 출력되는 내용은 같지만 둘은 완전히 다른 것이다.   
  따라서 b.push(3);
  을 하면  

  <pre>
  a = [1, 2];   
  b = [1, 2, 3];  
  </pre>

  이 된다.   

  그렇기 때문에 평소에 push를 쓰고싶다면 Array.from 을 사용하면 된다.   

  <br>

  `Array.from(this.state.contents)`  
  후에 새로운 변수에 담아주고 이 것을 setState에 넣어 변화를 주면 된다.   

  <pre>
    //Array.from 쓰기
    var newContents = Array.from(this.state.contents);
    newContents.push({id:this.max_content_id, title:_title, desc:_desc});
    this.setState({
      contents: newContents
    });
  </pre>

  <br>

  **Array.from**은 배열 복제 에만 사용할 수 있고  
  객체 복제할때는 **Object.assign**을 쓸 수 있다.   


  <pre>
  var a = {name:'egoing'};  
  var b = Object.assign({}, a);  ※ 첫번째 인자로는 빈 객체 혹은 값을 삽입할 객체를 넣으면 된다.  
  </pre>

  하면 a 와 b 는 가지고 있는 내용은 같지만 두 개는 서로 같은 것이 아니게 된다.  
 
  <pre>
  console.log(a, b, a===b)
  {name: "egoing"} {name: "egoing"} false
  </pre>
  
  유사배열, 유사 객체

  참고합시다.

  [SCOTCH]("https://scotch.io/tutorials/using-immutablejs-in-react-redux-applications")
  [immutable-js]("https://github.com/immutable-js/immutable-js")