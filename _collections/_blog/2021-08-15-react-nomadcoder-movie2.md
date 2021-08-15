---
layout: post
title:  "[React] 필모그래피 영화 앱 만들기 7"
author: Kenna
date:   2021-08-15 12:26:35 +0830
image: https://images.unsplash.com/photo-1591267990439-bc68529677c3?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1336&q=80
rating: 52
description: React로 영화 앱 만들기
categories : React
tags: React
---
<br>

###### HTML 마크업하기

<br><br>

App 컴포넌트가 로딩하는 큰 부분을 section으로 처리하고  
isLoading 삼항 연산자의 각 표현식 부분을 div로 묶어준다. (각각의 부분을 괄호로 묶어주면 더 가독성이 좋다)  
특히 map으로 나오게 될 movies는 ul>li로 구성한다.  

*HTML 태그 안에 자바스크립트 코드가 들어가게 된다면 (ex movies.map()...) 반드시 { }중괄호로 묶어줘야 한다.

<br>

```
//App.js
//강의에서는 ul>li 구성을 하지 않았는데 나는 추가로 필요할 일이 있을 것 같아 리스트로 마크업했다.  

render(){

    const { isLoading, movies } = this.state;
   
    return <section className="container">
      {
        ( isLoading ) ? 
        ( 
        <div className="loader">
          <span className="loader">Loading...</span>
        </div> 
        ) : 
        ( 
        <div className="movies">
          <ul>
            {movies.map ( movies=> {
              return <li>
              <Movie 
              id={movies.movieCd} 
              title={movies.movieNm} 
              key={movies.movieCd} />
              </li>
            })}
          </ul>
        </div>
        )
      }
    </section>
  }
}
```

그리고 제목이 표시되는 `{ title }`과 `{ year }` 이 있는 Movie 컴포넌트도 마크업을 수정한다.  
나는 별도의 이미지가 없기 때문에 나중에 이미지를 추가할 수 있는 `movies_img_box`라는 div 박스를 하나 넣어주었다. 

<br>

```
//Movie.js

import React from 'react';
import PropTypes from 'prop-types';
 
function Movie({id, year, title}){
    return <article className="movies_info">
        <div className="movies_img">
            <div className="movies_img_box">images</div>
        </div>
        <div className="movies_text">
            <h4 className="movies_title">{ title }</h4> 
            <p className="movies_year">{ year }</p> 
        </div>
    </article>
}

Movie.propTypes = {
    id : PropTypes.string.isRequired,
    year : PropTypes.string.isRequired,
    title : PropTypes.string.isRequired,
}

export default Movie;
```
<br><BR>

###### CSS 적용하기

<br><BR>

나는 수업과 달리 CSS를 SASS/SCSS로 적용할 계획이기 때문에
`npm i node-sass` 를 이용해 SASS/SCSS 를 사용할 라이브러리를 다운받는다.  

그리고 VScode에서 Sass 전처리기를 켜고.. (확장에서 설치 가능) 
css 폴더를 만들어 Scss 파일을 만든다.  

그리고 css 작업을 해주면 된다.

<br>
<br>


