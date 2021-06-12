---
layout: post
title:  "[Javascript DOM] 비동기 프로그래밍"
author:  Kenna
date:   2021-05-20 15:40:35 +0830
image: https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Ftse2.mm.bing.net%2Fth%3Fid%3DOIP.dG-yexYrhUA2RommlI9TmQHaEK%26pid%3DApi&f=1
rating: 7
description: MDN 문서 | 일반적인 비동기 프로그래밍 개념
categories : [DOM]
tags: [DOM]
---


###### 비동기 프로그래밍 Asynchronous
[MDN 보러가기]("https://developer.mozilla.org/ko/docs/Learn/JavaScript/Asynchronous/Concepts")

###### '비동기적Asynchronous' 이란?

일반적인 프로그램의 코드는 순차적으로 (위에서 아래로 한 줄 씩) 실행된다. 
하지만 어떤 작업을 수행하는 동안 다른 작업을 수행 할 수 있게 하는 것이 비동기 프로그래밍의 기본이다.

웹에서 이러한 작업을 비동기적으로 실행할 수 있는 API를 제공하는 것은 웹브라우저에 달려있다.

**Blocking code**<br>

웹 앱이 브라우저에서 특정 코드를 실행하느라 브라우저에게 제어권을 돌려주지 않으면 브라우저는 멈춘 것처럼 보인다.

사용자 입력을 처리하느라 웹 앱이 프로세서에 대한 제어권을 브라우저에게 반환하지 않는 이러한 현상이 **Blocking**이다.

-> 이러한 현상은 자바스크립트가 기본적으로 **single threaded** 이기 때문이다.


###### thread

기본적으로 프로그램이 작업을 완료하는데 사용할 수 있는 단일 프로세스로
각 스레드는 한 번에 하나의 작업만 수행 가능하다.

<pre>
<code>
Task A -> Task B --> Task C
</code>
</pre>

A 작업을 완료해야 B 작업을 수행할 수 있다.

Multiple thread를 지원하는 프로그래밍 언어는 멀티코어 CPU를 사용하여 여러 작업을 동시에 처리할 수 있다.

자바스트립트는 main thread라고 불리는 단일 thread에서만 작업을 실행할 수 있다.
이러한 문제를 해결하기 위해 worker라고 불리는 별도의 스레드로 작업을 보낼 수 있다.

따라서 시간이 오래 걸리는 작업은 worker를 이용해 처리하면 blocking 발생을 막을 수 있다.
그러나 worker는 DOM에 접근할 수 없고 단순히 숫자만 계산하며 동기적으로 실행된다.

<pre>
<code>
Main thread   : Task A -> Task B ----> | Task D |
Worker thread : Task C ============> |        |
</code>
</pre>

Task D가 B와 C의 결과를 모두 사용한다고 가정했을 때 두 개의 결과가 모두 들어오지 않으면 에러가 발생된다.

이 문제를 해결하기 위해 
**Promises**를 사용한다.

<pre>
<code>
Main thread   : Task A                 Task B 
    Promise   :   |____async operation ___|
</code>
</pre>

브라우저를 통해 특정 작업을 비동기적으로 실행하게 한다. 따라서 Task A 가 자기 작업을 수행하는 동안 Task B를 기다리게 할 수 있다.

이 작업은 다른 곳에서 처리가 되므로 비동기 작업이 진행되는 동안 main thread가 차단되지 않는다.