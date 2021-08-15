---
layout: post
title:  "[React] 필모그래피 영화 앱 만들기 6"
author: Kenna
date:   2021-08-15 12:26:35 +0830
image: https://images.unsplash.com/photo-1591267990439-bc68529677c3?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1336&q=80
rating: 51
description: React로 영화 앱 만들기
categories : React
tags: React
---
<br>

###### state 설정하기
<br>
<br>

컴포넌트 생명주기함수에서 가장 처음으로 컴포넌트가 mount 될 때 보여줄 state는  
isLoading이다.  
브라우저가 데이터를 가지고 오는 시간을 벌어준다.  

<br>

```
  state = {
    isLoading: true,
  }
```
<br>
위와 같이 state에 isLoading이라는 state를 주고 값을 true로 설정한다.
그리고 렌더 함수에 isLoading이 참이면 화면에 'isLoading...' 이라는 문구를 출력하도록  
그리고 거짓이면 'We are Ready'라는 문구가 보이도록
삼항연산자 조건문을 설정한다. 

<Br>

render()의 return안에 자바스크립트를 작성할 때는 **중괄호{ }**

<br>

```
render(){
   
    return <div>
      <p>{
        this.state.isLoading ? "Loding..." : "We are Ready!"
      }</p>
    </div>
  }
```

<br>

이 때 구조분해 할당으로 `this.state.isLoading`을 변경할 수 있다. (저번에 했던)  
return 전에 변수로 this.state의 isLoading을 불러올 수 있다.  

```
  render(){

    const { isLoading } = this.state; //변수 선언
   
    return <div>
      <p>{
        isLoading ? "Loading..." : "We are Ready!"
      }</p>
    </div>
  }
  ```

  <br>

맨 처음 render()함수를 호출하면 생명주기함수로 어떤 것이 올까?  
컴포넌트가 마운트 되었으니 마운트 되었다고 알려주는 *componentDidMount()* 함수가 온다.  

<br>

이 componentDidMount()함수를 이용해 'Loading...'이라는 문구가 일정 시간 이후에  
'We are Ready'로 바뀔 수 있도록 setTimeout을 넣을 수 있다.  

```
componentDidMount(){                   //컴포넌트가 마운트 되면
 setTimeout(                           //setTimeout 이벤트리스너를 실행하고
 () => {                               //화살표 함수를 실행하는데
 this.setState({isLoading : false})    //this에 state isLoading을 false 로 변경
 }, 6000)                              //6000 밀리초 이후에  
}
```

<br>

실제 할 일은 componentDidMount 시 data를 넣는 것이다.  
movies라는 state를 선언하고 빈 배열을 값으로 설정한다.

*팁 : setState 안에는 미리 사용할 값들을 넣어두어도 상관없다.  
    state안에 defalut 값을 일일이 지정할 필요는 없다.

<br>

```
  state = {
    isLoading: true,
    movies: [],
  }

```
<br>
<br>

###### 데이터 fetch 하기  

<Br><br>

일반적으로 자바스크립트로 데이터를 가져오는 방법은 fetch이다.  
하지만 더 나은 방식은 Axios다.  

<br>

`npm install axios` 를 사용해 axios를 설치한다.  

*노마드코더에서는 YTS라는 사이트의 영화 api 를 사용했는데, 나는 다른 영화앱을 제작하기 위해 '한국영화진흥원'의 api를 사용한다.  
*추가로 '케이트 블란쳇' 배우의 앱을 만들기 위해 code를 입력한 영화인 검색 api를 사용한다.

`https://kobis.or.kr/kobisopenapi/webservice/rest/people/searchPeopleInfo.json`

<br>

URL을 얻게 되면 axios를 import 한다.  
`import axios from "axios"`

<Br>

그리고 componentDidMount()에 axios.get()로 api를 넣어준다.  
api에서 데이터를 잡아야 state에 사용할 수 있다.  
하지만 axios를 쓰면 항상 빠르게 데이터를 가져오지 않는다.  
화면이 렌더링 되는 속도보다 데이터를 가져오는 것이 느리면 화면이 정상적으로 출력되지 않을 수 있기 때문이다.  

<br>

따라서 자바스크립트에게 componentDidMount()가 완료 된 다음 다른 작업을 수행하라고 알려줘야 한다.  
<br>
<br>

###### 스크립트 기다려!

<br>
<br>

`async`를 componentDidMount() 함수 앞에 붙이는 방법이 있다.  

```
async componentDidMount(){
}
```
<br>

그리고 axios를 직접 componentDidMount()에 넣지 말고 새로운 함수를 만들어서 넣어주는 방법도 있다.  
  
  
```
getMovies = async () => {
    const movies = await axios.get("api 주소");
  }

componentDidMount(){
    this.getMovies();
}
```
<br>

이것은 비동기적으로 api를 불러올 수 있게 해준다.  
함수를 실행할 때 async를 붙여주고, axios를 가지고 올 때 await를 붙여주면 axios가 실행될 때까지 기다렸다가 다음 일을 재개한다.  

<br>


`리액트는 렌더 함수를 실행한다.`  
`componentDidMount() 함수를 실행한다.`  
`componentDidMount() 안의 getMovies 함수를 실행한다.`  
`getMovies는 데이터를 axios로 받아오는 함수로 비동기적async로 다 받아지기를 기다린다 await`
<br>
<br>


##### 가져온 데이터를 확인하고 렌더링 하기

<br>
<br>

getMovies 함수에 console.log로 api가 잘 가져와지고 있는지 확인해본다.    

  
```
  getMovies = async () => {
    const movies = await axios.get("api 주소");
    console.log(movies);
  }
```

<br>

console.log에서 우리가 필요한 것을 찾을 수 있다.  
강의에서는 `movies.data.data.movies`고 나의 경우는 `movies.data.peopleInfoResult.peopleInfo.filmos` 다.   
하지만 이건 너무 길고 ES6 버전 구조분해할당으로 바꿔줄 수 있다. 

<br>

```
console.log(movies.data.peopleInfoResult.peopleInfo.filmos);
```
는    

```
  getMovies = async () => {
    const { data: { peopleInfoResult : { peopleInfo : { filmos } } } } = await axios.get("api 주소");
    console.log(filmos);
  }
```
으로 바꿔줄 수 있다.  
<br>

이 객체로 이루어진 배열인 filmos를 state안에 넣어준다.   
미리 만들어 둔 state 의 `movies = [];` 에 { filmos }를 setState로 넣어준다.  
그리고 isLoading이 계속 true면 Loading... 만 표시되기 때문에  
isLoading도 false로 변경해준다.  
<br>
  
``` 
  getMovies = async () => {
    const { data: { peopleInfoResult : { peopleInfo : { filmos } } } } = await axios.get("api 주소");
    this.setState({movies : filmos, isLoading : false});
    //여기서의 movies는 state의 movies고 filmos는 axios의 filmos다. 
  }
```

<br>  
이렇게하면 setTimeout을 쓰지 않아도 movies에 filmos를 불러오는게 완료되면  
isLoading이 false 상태가 된다.  

이제 Movie.js 파일을 만들어 실제 api 데이터를 렌더링 해준다.  
Movie 컴포넌트는 state를 필요로 하지 않기 때문에 (동적인 변화가 없음)  
state는 사용하지 않는 함수형 컴포넌트를 사용해도 된다.   

props만 쓰기 때문에 Movies.propsTypes를 이용해서  
props의 타입들을 미리 지정한다.  

```
Movie.propTypes = {
    id : PropTypes.number.isRequired,
    moviecode : PropTypes.number.isRequired,
    title : PropTypes.string.isRequired,
}
```
<Br>
<br>

*참고로 영화api를 이용하기 위해 필요한 배우코드, 영화코드들은 [영화진흥위원회 DB찾기]("https://www.kofic.or.kr/kofic/business/infm/introData.do") 에서 확인할 수 있다.  

**peopleInfo의 filmos에서 내가 가져올 수 있는 것은 영화코드, 영화제목, 영화참여분야 뿐으로 id 값은 영화 코드로 삽입하고 이미지 등은 별도로 처리할 계획이다.


<br>
<br>


###### Movie 컴포넌트에 데이터 가져오기

<br>
<br>

이제 App 컴포넌트에 Movie 컴포넌트를 가지고 와서 렌더링 해줘야 한다.   
<br>

```
//Movie.js

import React from 'react';
import PropTypes from 'prop-types';
 
function Movie({id, year, title}){
    return <h4>
        { title }
    </h4>
}

Movie.propTypes = {
    id : PropTypes.string.isRequired,
    year : PropTypes.string.isRequired,
    title : PropTypes.string.isRequired,
}

export default Movie;
```

<br>

렌더링을 위해 movies state를 **map()** 함수로 반환해줘야 한다.   
render() 안에 movies를 변수로 받아서 
movies에 map 함수를 붙이고   
이 객체를 movies라는 인자로 받아서  
화살표 함수에 return으로 Movie 컴포넌트와 props를 넣어준다.  

<br>

```
render(){

    const { isLoading, movies } = this.state; //movies를 state에서 가져와야한다.
    //this.state.movies도 가능하지만 위의 방법이 낫다.
   
    return <div>
      {
        isLoading ? "Loading..." : movies.map(movies=>{
          console.log(movies.movieNm);
          return <Movie id={movies.movieCd} title={movies.movieNm} key={movies.movieCd} />
          //상단에 Movie 컴포넌트를 import 해주자

        })
      }
    </div>
  }
}
```
<br>
<br>


내가 필요한 props는 title과 movieCd뿐이라 props는 title과 movieCd 뿐이고  
이 **props를 Movie.js 컴포넌트에 전달해 Movie 컴포넌트가 값을 출력**하도록 만든다.  
<br>
 
*중괄호를 확인하자!!
**현재 기본적으로 연도별 sort 되어 있어 sort는 설정하지 않았다.
***key의 경우 리액트만 확인하면 되기 때문에 개별 영화 코드인 movieCd를 key props로 설정했다.  

<br>

와 나도 API에서 데이터를 가져올 수 있다!

<br>
<img src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fattach.s.op.gg%2Fforum%2F20171223172341_140854.jpg&f=1&nofb=1" alt="너두?">
야 나두!

<br>
<br>


