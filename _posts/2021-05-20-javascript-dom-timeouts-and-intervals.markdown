---
layout: post
title:  "[Javascript DOM] timeouts 과 intervals"
author:  Kenna
date:   2021-05-20 16:20:35 +0830
image: https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Ftse2.mm.bing.net%2Fth%3Fid%3DOIP.dG-yexYrhUA2RommlI9TmQHaEK%26pid%3DApi&f=1
rating: 6
description: MDN 문서 | Cooperative asynchronous JavaScript - Timeouts and intervals
categories : [DOM]
tags: [DOM]
---


###### timeouts 과 intervals
[MDN 보러가기]("https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Timeouts_and_intervals")

###### setTimeout()
지정된 시간이 경과 한 후 (ms 단위) 지정된 코드 블록을 한 번 실행한다.

<pre>
<code>
window.setTimeout(호출할 함수, 지연 시간);
</code>
</pre>

**clearTimeout()**<br>
settimeout() 메소드의 반환값을 clearTimeout() 메소드의 인수로 전달하면, 계획된 함수의 호출을 취소할 수 있다.


###### setInterval()
지정된 시간 간격만큼 지정된 코드 블록을 반복해서 실행한다. 애니메이션과 같이 코드를 일정한 시간 동안 반복해야 할 때 사용한다.

<pre>
<code>
window.setInterval(호출할 함수, 지연 시간);
</code>
</pre>

**clearInterval()**<br>
setInterval() 메소드의 반환값을 clearInterval() 메소드의 인수로 전달하면, 반복되는 함수의 호출을 취소할 수 있다.

###### setTimeout() 함수와 setInterval() 사이의 차이점

- setTimeout()은 코드 실행 사이의 지정한 시간을 보장한다. 해당 코드가 실행 완료된 후에 다시 호출을 하므로 코드 실행에 걸리는 시간은 제외된다.

- setInterval()의 경우 지정한 시간(ms단위) 안에는 코드 실행 시간이 포함된다. 실행에 40ms 가 걸리는 함수의 인터벌 시간으로 60ms 지정 시 실제 간격은 20ms에 불과하다.


###### requrestAnimationFrame()
최신 버전의 setInterval()로 브라우저가 디스플레이를 다시 렌더링 하기 전에 지정된 코드 블록을 실행하여 애니메이션이 실행되는 환경에 관계없이 적절한 프레임 속도로 실행되도록 한다.



**>> 위의 함수들은 과용하게 되면 페이지 속도를 느리게 할 수 있다. 모두 메인 스레드에서 실행된다.**