---
layout: post
title:  "[React] 필모그래피 영화 앱 만들기 9"
author: Kenna
date:   2021-08-16 20:26:35 +0830
image: https://images.unsplash.com/photo-1591267990439-bc68529677c3?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1336&q=80
rating: 54
description: React로 영화 앱 만들기
categories : React
tags: React
---
<br>

###### Home 컴포넌트 변경하기

<br><Br>

개인적으로는 Home은 Home 대로 MovieList는 MovieList 대로 구성되는 것이 좋아  
nav에 들어가는 라우팅 포인트가 총 3개였으면 했다.  

현재 들어가있는 제목 아래에 nav가 들어가고  
총 3개의 component (Home, About, Filmos) 로 라우팅 포인트를 나눴다.  

<br>

```

class App extends React.Component {
render(){
  return (
    <section className="main_container">
    <h1 className="main_title">Cate Blanchett</h1>
      <HashRouter>
        <Navigation />
      <Route path="/" exact={true} component={Home} />       //Home 컴포넌트
      <Route path="/movielist" exact={true} component={MovieList} />  //MovieList 컴포넌트 (Filmos)
      <Route path="/about" exact={true} component={About} /> //About 컴포넌트
      </HashRouter>
  </section>  
)}
}
export default App;

```

<br><br>

**Home 컴포넌트**   
애플리케이션의 목적과 내 소개가 들어가는 컴포넌트
URL path가 "/"이 되어 index로 쓰인다.  
<br>

**About 컴포넌트**   
배우 케이트 블란쳇의 소개 페이지  
<br>

**MovieList 컴포넌트**   
배우 케이트 블란쳇의 필모그래피 리스트
<br>

이렇게 구분했고 
기존의 `Home.js` 파일이 `MovieList.js` 파일로 이름이 변경되었다.  
그리고 `Home.js` 파일을 새로 만든 다음 컴포넌트를 만들었고  
마크업과 디자인 작업을 하였다.  

<br>
<br>

###### router props

<br>
<br>

리액트의 라우터 컴포넌트로 인해 만들어진 props가 있다.  
<br>

```
{history: {…}, location: {…}, match: {…}, staticContext: undefined}
history: {length: 50, action: "PUSH", location: {…}, createHref: ƒ, push: ƒ, …}
location: {pathname: "/about", search: "", hash: "", state: undefined}
match: {path: "/about", url: "/about", isExact: true, params: {…}}
staticContext: undefined
```
<br>

라우터에 있는 모든 라우트는 history, location, match, staticContext 네 가지의 props를 기본적으로 가지고 있다.  
라우터를 사용할 때 이 네 가지의 props를 사용할 수 있다.  
`<Link to="">` 의 to 를 state 객체 형태로 바꾼 다음 각 컴포넌트에 props로 보낸다.  

<br>

```
//Navigation.js

import React from 'react';
import { Link } from 'react-router-dom';
import '../css/Navigation.css';

function Navigation(){
    return (<section className="nav">
        <Link to="/" className="nav_home">Home</Link>
        <Link to={{ pathname: '/about',
                    state:{ fromNavigation: true },
        }} className="nav_about">About</Link>
        <Link to="/movielist" className="nav_movielist">Filmos</Link>
    </section>)
}
export default Navigation;
```

이런 형태로 Link를 변형하면 된다.  
실제 디테일을 구현할 Movie 컴포넌트로 가서 link를 import 한다.  
현재 Movie 컴포넌트는 div로 묶여 있는데 이 전체를 `<Link to={{}}>` 로 감싸준다.  

이렇게 하고 나면 이것들을 클릭할 때 마다 state 형태로 props가 전달되게 된다.

<br>

```
class Movie extends React.Component{
    render(){
    const {year, title} = this.props;

    return ( <Link to={{
        pathname: '/movie-detail',
        state: {year, title}
    }}>
    <article className="movies_info">
        <div className="movies_text">
            <h4 className="movies_title">{ title }</h4> 
            <p className="movies_year">{ year.slice(0,4) }</p> 
        </div>
    </article>
    </Link>) 
    }
}
```
<br>

이렇게 하면 칸칸마다 선택하는 경우 링크 클릭이 가능해지고 위의 props도 전달된다.  

<br>

그리고 `App.js`안의 라우터에 Detail 컴포넌트를 넣어주고(상단에도 import)  
`Detail.js` 컴포넌트를 만든다.

그리고 컴포넌트를 만든 후 console.log(props)를 찍어보면  

<br>

```
location:
hash: ""
pathname: "/movie-detail"
search: ""
state: {year: "20206362", title: "어디갔어, 버나뎃"}
[[Prototype]]: Object
```
<br>

이렇게 state가 잘 넘어온 것을 볼 수 있다. 
위의 location 부분을 구조분해할당 하여 function Detail 컴포넌트에서 사용할 수 있다.  

하지만 이전에 주소를 직접 친다던지하여 각 제목을 클릭해서 Detail 컴포넌트로 넘어오지 않아 state 값이 없으면 props undefined 오류가 뜬다.  
이 경우를 해결하기 위해 리다이렉트 기능을 사용한다.  

<br><Br>

###### 리다이렉트 기능 만들기  

<br><Br>

이전의 Detail 컴포넌트를 class 컴포넌트로 변환하고  
this.props로 location을 받아와 state를 출력해본다.  

<br>

```
import React from 'react';

class Detail extends React.Component{
    componentDidMount(){
        const {location} = this.props;
        console.log(location.state)
    }
    render(){
        return (<div>

        </div>)
    }
}
export default Detail;
```

<br>

이 경우에도 movie-detail을 주소창에 치면 값은 undefined고  
카드를 눌러 들어오면 값을 확인할 수 있다.  
그래서 location의 state 값이 undefined면 다시 뒤로 돌아가도록 (movie-detail을 확인할 수 없도록 해야한다.)  

아까 확인한 props 중에는 history 키가 있는데 여기에 **push 메소드**를 이용하면 방금 전 url을 얻어낼 수 있다.  
<br>

```
{history: {…}, location: {…}, match: {…}, staticContext: undefined}
history:
action: "PUSH"
block: ƒ block(prompt)
createHref: ƒ createHref(location)
go: ƒ go(n)
goBack: ƒ goBack()
goForward: ƒ goForward()
length: 50
listen: ƒ listen(listener)
location: {pathname: "/movie-detail", state: {…}, search: "", hash: ""}
push: ƒ push(path, state)
replace: ƒ replace(path, state)

```

그래서 location과 history를 둘 다 props로 받아 조건문이 참이 되면 push()를 이용해 홈으로 보내거나 다시 뒤로 보낼 수 있다.  


```
import React from 'react';

class Detail extends React.Component{
    componentDidMount(){
        const { location, history } = this.props;
        if ( location.state === undefined ){
            history.push('/movielist');
        }
    }
    render(){
        return (<div>

        </div>)
    }
}
export default Detail;
```
<br>

그리고 아래 render 에서는 받아온 props를 이용해서 값을 출력할 수 있다.  
<br>

```
  render(){
      const { location } = this.props;
      return (<div>
          {location.state.title}
      </div>)
  }
```
<br>

그런데 componentDidMount() 함수에 넣어 둔 리다이렉트는 컴포넌트가 마운트 될 때만 실행되고 render 안의 값이 변하거나 undefined일 때는 실행되지 않는다.  

그래서 render 안에도 리다이렉트 조건문을 넣어줘야 하는데 이 때 location.state가 값이 있다면 표시하고, 없으면 return null을 표시해 다시 돌아가게 하면 된다.  
<br>

```
import React from 'react';

class Detail extends React.Component{
    componentDidMount(){
        const { location, history } = this.props;
        if ( location.state === undefined ){
            history.push('/movielist');
        }
    }
    render(){
        const { location, history } = this.props;
        if (location.state){
        return <div>
            {location.state.title}
            </div>
        }else{
            return null
        }
    }
}
export default Detail;
```



<br>
<br>

여기까지가 책의 마지막이고  
이제는 내 식대로 마무리 해보려고 한다.  
<br>
<br>








Movie Detail 컴포넌트를 만들어야 하는데..  
내가 쓰는 api는 영화 상세 정보가 별도로 나오지 않는다.  
(차라리 YTS의 컴포넌트를 쓸걸 그랬나? 이미지가 나오면 좋겠는데ㅜㅜ)  


