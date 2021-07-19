---
layout: post
title:  "생활코딩 : 머신러닝 야학 2. 2"
date:   2021-01-06 17:53:33 +0830
image: https://images.unsplash.com/photo-1495592822108-9e6261896da8?ixid=MnwxMjA3fDB8MHxzZWFyY2h8M3x8bWFjaGluZSUyMGxlYXJuaW5nfGVufDB8fDB8fA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60
rating: 6
---

###### 머신러닝야학2기 - 텐서플로우 Javascript (2)



***DAY 2 : ~나의 모델 만들기***

---
<br>

###### 강의 1

1. **과거의 데이터 준비**

    var 온도 = [**20,21,22,23**];

    var 판매량 = [**40,42,44,46**];

    **텐서플로우는 배열을 '텐서'로 변환해야 한다.**

    var 원인 = tf.tensor(온도);

    var 결과 = tf.tensor(판매량);
<br>

2. **모델의 모양을 만든다**

    var X = tf.input({ shape: [**1**] });

    var Y = tf.layers.dense( { units: **1** } ).apply(x);

    var model = tf.model({ inputs: X, outputs: Y });

    var complieParam = {optimizer: tf.train.adam), loss: tf.losses.meanSquaredError}

    model.compile(compileParam);
<br>

3. **데이터로 모델을 학습(FIT) 한다.**

    var fitParam = **{epochs:100}**

    model.fit(원인, 결과,        ).then(funtion(result){

    var 다음주온도 = [**15,16,17,18,19**]

    var 다음주원인 = tf.tensor(다음주온도,[다음주온도.length,1]);

    var 다음주결과 = model.predict(다음주원인);

    다음주결과.print();

    });
<br>

4. **모델을 이용한다.**

![model](%E1%84%86%E1%85%A5%E1%84%89%E1%85%B5%E1%86%AB%E1%84%85%E1%85%A5%E1%84%82%E1%85%B5%E1%86%BC%E1%84%8B%E1%85%A3%E1%84%92%E1%85%A1%E1%86%A82%E1%84%80%E1%85%B5%20-%20%E1%84%90%E1%85%A6%E1%86%AB%E1%84%89%E1%85%A5%E1%84%91%E1%85%B3%E1%86%AF%E1%84%85%E1%85%A9%E1%84%8B%E1%85%AE%20Javascript%20(2)%207e96c0cec2bb476d815f3ed58b5cdb18/Untitled.png)
<br>

###### 강의 2

<br>

**[텐서플로우 설정하기](https://www.tensorflow.org/js/tutorials/setup?hl=ko)**

<br>

###### 강의 3
<br>

지도학습을 하기 위해서는 데이터를 원인(독립변수)과 결과(종속변수)로 구분해야 한다

코드로는 이렇게 표현한다.

```jsx
var 온도 = [20,21,22,23];
var 판매량 = [40,42,44,46];
```

텐서플로우에서는 이렇게 변환해줘야한다.

```jsx
var 원인 = tf.tensor(온도);
var 결과 = tf.tensor(판매량);
```

```jsx
// 1. 과거의 데이터를 준비합니다. 
        var 온도 = [20,21,22,23];
        var 판매량 = [40,42,44,46];
        var 원인 = tf.tensor(온도);
        var 결과 = tf.tensor(판매량);
```

###### 강의 4
<br>

모델의 모양 만들기

```jsx
// 2. 모델의 모양을 만듭니다. 
        var X = tf.input({ shape: [1] });
        var Y = tf.layers.dense({ units: 1 }).apply(X);
        var model = tf.model({ inputs: X, outputs: Y });
        var compileParam = { optimizer: tf.train.adam(), loss: tf.losses.meanSquaredError }
        model.compile(compileParam);
```
<br>

###### 강의 5

모델의 실제 내용이 되는 수학적 공식 만들기 - FIT

epochs 값만큼 학습을 반복한다.

```jsx
// 3. 데이터로 모델을 학습시킵니다. 
        var fitParam = { epochs: 100} 
        var fitParam = { epochs: 100, callbacks:{onEpochEnd:function(epoch, logs){console.log('epoch', epoch, logs);}}} // loss 추가 예제
        model.fit(원인, 결과, fitParam).then(function (result) {
            
         });
```
<br>

###### 강의 6

predict(원인)에 우리가 학습 시킬 때 사용했던 온도 데이터를 넣어준다.

```jsx
// 3. 데이터로 모델을 학습시킵니다. 
        var fitParam = { epochs: 100} 
        var fitParam = { epochs: 100, callbacks:{onEpochEnd:function(epoch, logs){console.log('epoch', epoch, logs);}}} // loss 추가 예제
        model.fit(원인, 결과, fitParam).then(function (result) {
            
            // 4. 모델을 이용합니다. 
            // 4.1 기존의 데이터를 이용
            var 예측한결과 = model.predict(원인);
            예측한결과.print();

        // });  

        // 4.2 새로운 데이터를 이용
        var 다음주온도 = [15,16,17, 18, 19]
        var 다음주원인 = tf.tensor(다음주온도);
        var 다음주결과 = model.predict(다음주원인);
        다음주결과.print();
```

<br>
<br>
<br>