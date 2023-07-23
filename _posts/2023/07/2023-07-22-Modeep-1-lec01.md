---
title: 모딥 시즌 1 - ML lec 01 
categories: [DeepLearning, 모두를 위한 딥러닝 시즌 1]
tags: [모두를 위한 딥러닝 시즌 1]
---

# lec 01 정리
## 목차 
- What is ML 
    - Supervised learning
    - Unsupervised learning
    - Supervised learning VS Unsupervised learning
- Training dataset
- Types of supervised learning 
    - Regression / Binary classification / multi-label classification

<br>

## What is ML
ML은 Machine Learning의 줄임말이다.  
ML이 나오게 된 이유는 `Explicit programming`가 불가능 하기 때문이다.  
Explicit programming을 명시적 프로그래밍이라고 부르는데 이는 개발자가 의도한 대로만 작동하는 프로그램을 말한다.  

예를 들어
> 사과를 산다 -> 비용을 지불한다  

같은 간단한 프로그램을 짤때는 Explicit programming을 사용하여 만들 수 있다.  

<br>

하지만 Explicit programming이 불가능한 경우도 있다.  

예를 들어
> 스펨 필터   
> 자율 주행

정도가 있다.  
어떤 방식으로 코드를 짜던지 간에 스펨 필터는 특정 문자열을 일일이 규칙을 적어줄 수도 없고,  
자율주행은 어떤 신호에는 어떻게 반응하고 하는 엄청난 경우의 수를 개발자가 생각하기는 어렵다.  
그래서 기계가 데이터를 보고 스스로 학습하면 어떨까? 라는 생각으로 1959년 Arthur Samuel이라는 사람이 ML을 만들게 되었다.  

ML이 학습하는 방법은 총 3가지로 나뉘지만 이번 강의에서는 2가지만 나와 2가지만 정리하겠다. 
- Supervised learning (지도 학습)
- Unsupervised learning (비지도 학습)

<br>

### Supervised learning (지도 학습)
지도 학습은 이미 레이블이 정의되어 있는 정해진 데이터를 학습한다.  
또 다른 의미로 training dataset, 학습 데이터 이라고 부르기도 한다. 

간단한 예시를 살펴보자면 

<img src="/assets/img/Modeep1/supervised.png" width="70%" height="50%">  

위 사진처럼 이건 강아지이다, 이건 고양이이다를 분류하는데에 ML이 쓰이며  
사진에는 cat, dog를 레이블링하여 학습이 가능하도록 한다.  
레이블링을 했다는 것은 지도학습이라는 것을 알 수 있다.  

### Unsupervised learning (비지도 학습)  
Unsupervised learning은 supervised learning과 다르게 주어지는 데이터 없이 혼자서 스스로 학습한다.  
예를 들면 google news에서 비슷한 뉴스끼리 묶어주는 프로그램이 있을 것이며,  
데이터를 보고 자기 혼자서 학습하기 때문에 레이블링이 필요 없다.  


### 아니 그럼 어떤게 더 좋은거야?  
- Supervised learning 장/단점
    - 정확도를 많이 높일 수 있다.  
    - 레이블링을 일일이 하기에는 너무 힘들다.  

- Unsupervised learning 장/단점 
    - 레이블링을 일일이 하지 않아도 되서 정말 편하다.  
    - 정확도가 많이 떨어진다.  

서로 장단점이 확실하기에 때에 따라서 자신이 원하는 방법으로 사용하도록 하자.

<br>

## Training dataset 
Training dataset을 Supervised learning에서 사용한다고 예를 들었을 때 아래와 같을 것이다.  

| X | Y | 
|:---:|:---:|
|1, 2, 3,| 1|
|2, 3, 4| 2|  

X를 특징 혹은 feature라고 부르며 Y는 정답 레이블이라고 한다.  
만약 내가 만든 ML 모델이 위 데이터를 보고 학습 했다면 3, 4, 5라는 값을 주었을 때 Y는 3이라고 예측할 것이다.  

<br>

## Types of supervised learning
이제부터 모든 학습 방법을 Supervised learning이라고 가정하고 정리하겠다.  
사실은 교수님이 그렇게 한다고 영상에서 말씀하셨다.  

모델이 예측하는 방법도 여러가지로 나뉘어 진다.  
예를 들면 
> 공부한 시간에 따른 시험 점수 예측   
> 고양이와 강아지 분류   
> 고양이, 강아지, 토끼, ... 분류    

이런식으로 나눠볼 수 있는데  
X라는 데이터를 학습하여 점수를 예측하는 Regression
고양이와 강아지처럼 둘 중 하나만 분류하는 Binary classification   
여러 개 중에서 하나만을 분류하는 Multi-lable classification

이렇게 분류해볼 수 있다.

### supervised learning의 예측을 예시로 들어보자
예를 들어서 공부 시간에 따른 시험 점수를 예측한다고 해보자.  
그리고 Training dataset은 아래와 같다.  

| X(hour) | Y(score)| 
|:---:|:---:|
|10|90|
|9|80|
|3|50|
|2|30|

10시간을 공부하면 90점을 맞고, 9시간을 공부하면 80점을 받는 training dataset이 있다.   
위 raining dataset을 가지고 모델을 학습시켜서 7시간을 공부했다고 한다면
그 모델은 70점 정도를 예측할 것이고  
`Regression` 모델이 된다.  

<br>

또 예를 들어서 공부 시간에 따른 자격증 합격을 예측한다고 해보자

| X(hour) | Y(pass / fail)| 
|:---:|:---:|
|10|P|
|9|P|
|3|F|
|2|F|

그럼 위 training dateset과 데이터는 같지만 Y는 다르다.  
위 모델은 N개 중에서 하나만을 예측하는 것이기 때문에 Classification이 되고, 
그 중에서 두개 중에서 하나만을 분류하는 것이기 때문에 `Binary classification`이 된다. 

<br>

이제 마지막으로 하나가 남았는데 뭔지 알거라고 생각한다.

| X(hour) | Y(grade)| 
|:---:|:---:|
|10|A|
|9|B|
|3|C|
|2|D|

위 training dataset의 Y값은 총 4개이기 때문에 Classification 문제가 되고,  
여러개 중 하나이기 때문에 `Multi-label classification` 문제가 된다.

<br>

## 끝
이제 다음 강의 lec 02를 정리해보도록 하겠다.  
정리를 하면서 강의에서 나오지 않았던 것들도 추가로 적었기 때문에 잘못된 부분이 있을 수도 있는데 
잘못된 부분이 있다면 말해주세요..