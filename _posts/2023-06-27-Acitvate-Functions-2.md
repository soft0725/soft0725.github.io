---
title: 활성화 함수 Activate Function에 대해서 알아보자 - 2
date: 2023-06-27 10:55:00 +0900
categories: [딥러닝 공부, 밑바닥부터 시작하는 딥러닝]
tags: [활성화 함수]
---

# 저번 글에서는 
저번 글에서는 활성화 함수가 어떻게 생겼고, 어떤 원리로 동작하는지에 대해서 그냥 간단하게 알아보았다.  

<br>

# 이번 글에서는 
요즘따라 많이쓰고 있는 Relu 활성화 함수에 대해서 알아볼까 한다.  
그리고 어떤 이유에서 sigmoid를 쓰지 않는 것인지 알아보도록 하겠다.

<br><br>

# 왜 Relu를 쓰는지 알려면 chain rule을 알아야 한다.
`Activate function - 1` 에서는 원리에 대해서 말하긴 했었다.  
하지만 그렇게까지 깊게 알아보진 않아서 이번에는 조금 깊게 들어가보려한다.  

> Step function은 빼고 설명한다는 점 참고 바란다. 

<br>

## chain rule이란? 
일단 여기서는 깊게 들어가지 않고 `수학` 카테고리를 또 따로 만들어서 설명할 예정이다. 
그러니까 간단하게만 알아보자면 그냥 미분하기 어려운 함수를 여러개로 쪼개서 미분한 함수라고 생각하면 된다.  
그러면 앞에거때서 미분하고, 뒤에서 또 나눠서 미분하고, 계속 미분한다는 거다.  

[혁펨하임의 연쇄법칙](https://www.youtube.com/watch?v=g-Dz1YS58XM&list=PL_iJu012NOxea6yN2PUzw8hQ2Aniog8ql&index=7)

내가 말하는 것보다 혁펜하임님의 설명이 더 좋아서 chain rule을 모른다면 여길 참고바란다.  

<br><br>

# 자 이제 깊게 들어가보자 
앞에서 chain rule을 이해했다면 알 것이다.  
chain rule는 back propagation에서 쓰는 방법인데, 이때 Sigmoid와 Relu를 쓴다. 
그리고 chain rule을 쓰면 각각 곱해지게 되는데 이때 sigmoid의 가장 큰 문제점이 생긴다.  
앞에서 말했던 것 처럼 `sigmoid function은 값이 작으면 작을 수록 0에 가까워진다고 하였다.`
그래서 0.000000과 같은 수들을 계속해서 곱하게 되는데 그렇게 되면 back propagation을 할 때 
마지막에는 0과 같은 수가 되어버려 쓸모가 없다는 것이다.

<br>

## 아직도 이해 못하겠다면 코드로 보자  

### Sigmoid 에 아주 작은 값을 넣어보자 

결국에 내가 하고싶은말은 계속 곱해지게 된다면 어떤 문제점이 발생할까라는 것이다.  
```python
x = np.array([-5, -9, -19])

def sigmoid_function(x):
    return 1 / (1 + np.exp(-x))

sigmoid_y = sigmoid_function(x)

print(sigmoid_y)
```
위 코드를 실행시키면 [6.69285092e-03 1.23394576e-04 5.60279641e-09] 라는 값이 나온다.  
이 숫자들은 0.000232939 과 같은 매우 작은 숫자이다.  
그리고 이것을 다 곱하면 [4.6271338550503814e-15]의 값이 나온다.  
`이 값이 얼마나 작은거냐면 그냥 값이 0이다.`

<br>

### 반면에 Relu 는??

```python
def relu_function(x):
    return np.maximum(0, x)

relu_y = relu_function(x)

print(relu_y)
```

그냥 [0 0 0]이 나온다. 
그러면 아무리 backpropagation을 하더라도 어짜피 0이기 때문에 아무런 의미가 없다는 것이다. 
그래서 다들 Relu를 쓰는 것이다.   
따라서 현 시대에 딥러닝에 가장 적합한 활성화 함수는  
> Relu 이다.

하지만 히든레이어가 2개 ~ 3개정도면 상관없다고 하니 2~3개 정도면 sigmoid도 한번 써보자