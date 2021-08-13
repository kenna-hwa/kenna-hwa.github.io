---
layout: post
title:  "[React] 필모그래피 영화 앱 만들기 4"
author: Kenna
date:   2021-08-13 16:26:35 +0830
image: https://images.unsplash.com/photo-1591267990439-bc68529677c3?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1336&q=80
rating: 50
description: React로 영화 앱 만들기
categories : React
tags: React
---
###### Prop-types 사용해서 유효성 검사하기
<br>
<br>


하위 컴포넌트는 상위 컴포넌트로부터 전달 받은 props의 값 타입이 정확하게 들어왔는지 확인할 필요가 있다.

이럴 때 사용하는 것이 prop-types이다.  

`npm i prop-types` 를 터미널에 입력해서 설치할 수 있다.   
<br>

설치 후 App.js에 import 한다.  
그리고 사용할 컴포넌트인 Food에 propTypes를 프로퍼티로 적용한다.

<Br>

*대소문자가 생각보다 중요하다. 반드시 **p**rop**T**ypes로 해야하고  
내부 프로퍼티들에는 또 **P**rop**T**ypes라고 해야한다!
<br>

```
Food.propTypes = {
  name : PropTypes.string.isRequired,
  picture : PropTypes.string.isRequired,
  rating : PropTypes.number.isRequired,
}
```
<br>

이런 식으로 적용하면 되고  
만약 rating에 string을 필요로 한다고 적었다면  
  `rating : PropTypes.string.isRequired,`

<br>

실제 rating에는 숫자 타입의 값이 들어가고 있기 때문에  
console에 에러 메세지가 출력될거다. (rating props에 string 타입이 올거라고 기대했는데 number가 들어오고 있다 ... )   
<br>
이걸 이용하면 미리 내가 계획한 props의 타입이 있고, 그것을 명시하고, 실제 props를 전달할 때 혹시 모르게 타입이 잘못 전달되는 오류를 잡아낼 수 있다.  

<br>

만약 값이 반드시 있어야 하는 것이 아니라면 .isRequired를 떼버리면 된다. 
  `rating : PropTypes.number,`

<br>
이렇게 하면 rating props는 있을 수도 있고 없을 수도 있는 props가 되는 것이다. (number타입이거나 undefined라는 뜻)  
다만 값의 타입은 체크할 수 있다.  

[React Proptype]("https://reactjs.org/docs/typechecking-with-proptypes.html")


<br><br><br>

###### State

<br>
<br>

state는 동적 데이터와 함께 작업할 때 만들어진다.  
state는 변화하는 데이터다.  

<br>

App.js의 App 컴포넌트를 **함수형** 에서 **클래스형**으로 바꾼다.

<Br>

```
function App(){

  return( 

  );
}
export default App;
```
<br>

**...**
<br>

```
class App extends React.Component {
  render(){

    return (

    );
  }
}
export default App;
```

<Br><br>

App 컴포넌트는 React의 Component 을 상속받아 컴포넌트 기능들을 가지고 온다.  
그리고 함수형과는 달리 return을 바로 가지지 않고  
render() 메소드를 통해 화면에 나타날 것들을 return 한다.  
react는 **자동적으로** 클래스 컴포넌트의 render() 메소드를 실행한다.  
그리고 class 컴포넌트는 **state**를 가진다!  

<br>

```
state = {

}
```
<br>

**=>** class형 컴포넌트에서 사용할 수 있는 state는 변하는 데이터고 객체다. 

<br>

state를 render() 메소드 안에 넣기 위해서는
**{this.state.name}** 과 같이 변수처럼 활용하면 된다.
<br>
<br>

###### 컴포넌트에서 state의 data를 바꾸기
<br>
<Br>

컴포넌트의 data를 바꿔보자.  
Javascript를 사용한다.  

클래스 컴포넌트 내부에 함수를 만든다.  
<Br>

```
  add = () => {
    console.log("Add");
  }
  minus = () => {
    console.log("minus")
  }
```
<br>

이것을 이용해 render() 메소드 안의 button을 이용해 숫자를 늘리고 줄여보려고 한다.  

<BR>

```
  render(){
    return <div>
      <h2>The number is {this.state.count}</h2>
      <button onClick={this.add}>Add</button>
      <button onClick={this.minus}>Minus</button>
    </div>
  }
```

<br>

**onClick**은 리액트가 가지고 있는 기본적인 이벤트리스너로 하나의 **props** 다.  
해당 엘리먼트를 클릭하면 지정한 동작이 실행된다.  
{this.add}처럼 함수를 사용할 수 있는데, this는 이 클래스 컴포넌트 전체를 가리키고 이 컴포넌트 내의 add라는 함수를 불러오는 것이다.  
<br>
{this.add()}처럼 쓰지 않는 것은 ()를 붙이면 onClick시가 아니라 즉시 실행되기 때문에 ()를 빼는 것.  

<br>
<br>

###### setState()로 data 변경하기

<br>

`Do not mutate state directly. Use setState() `  
위의 add 함수에 this.state.count로 직접 state 값을 바꾸려고 들면 리액트는 setState를 사용하라고 조언한다.  

state는 고정되어 있는 데이터가 아니지만  
매번 직접 손을 대서 수정하는 데이터도 아니고,  
직접 지목해서 수정할 수 있는 데이터도 아니다.  

<br>

state가 변한다는 것은 data가 변한다는거고 화면도 그에 맞춰서 동적으로 변화해야 한다.  
그런데 state의 데이터를 직접 변경하려고 하면 react는 변경 사실을 인지하지 못하고, render() 메소드도 새로 불러와지지 않는다. 즉, 화면이 변화하지 않는다는 의미다.  
그렇게 때문에 내가 onClick props를 이용해서 state에 변화를 주고 싶다면 **setState()**를 사용해야 한다.   

<br>


**setState()를 이용하면 리액트가 '화면을 재렌더링 하고 싶군' 하면서 state값을 다시 받아다가 render() 메소드를 다시 실행시켜준다.**

<br>

**state**는 객체다.  
따라서 this.state.count = 1; 이 아니라, **this.setState({count:1})**로 수정해준다.  

그리고 '현재' state의 값에 +1 혹은 -1 하기 위해서  

<Br>

```
  add = () => {
    this.setState({ count: this.state.count + 1 })
  }
  minus = () => {
    this.setState({ count: this.state.count - 1 })

  }
```

으로 count state를 바꿔준다.  

<br>
여기서 더 나은 방식으로 사용하려면
this.state.count 대신 this.state를 function의 값으로 받아와서 사용하는 방식으로 변경한다.  

<br>

```
  add = () => {
    this.setState(nowState => ({ count: nowState.count + 1 }));
  }
  minus = () => {
    this.setState(nowState => ({ count: nowState.count - 1 }))

  }
```

<br><Br>

**setState()는 호출할 때마다 변화한 state의 data를 가지고 render()메소드를 재호출한다.**
<br><Br>





