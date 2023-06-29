---
title: 활성화 함수 Activate Function에 대해서 알아보자 - 1
date: 2023-06-27 10:6:00 +0900
categories: [딥러닝 공부, 밑바닥부터 시작하는 딥러닝]
tags: [활성화 함수]
---


# Acitvate function의 종류 
---
## Step function [ 계단 함수 ]

계단 함수라고 불리는 Step function은 활성화 함수의 한 종류이며 주로 퍼셉트론에서 쓰인다.  
`Step function는 앞에서 입력받은 신호의 크기가 0미만이라면 0을 출력하고, 
0이상부터는 1로 출력하는 성질을 가지고 있다.`

### Code 
```python
def step_function(x):  
	return np.array(x > 0, dtype=np.int64)
```

코드를 보면 x를 입력받는다. 이때 x는 앞 퍼셉트론에서 받은 신호의 값이다.   
입력받은 신호의 값이 0보다 크다면 1을 작거나 같다면 0을 출력한다.  
마지막으로 dtype=np.int64를 달아준 이유는 퍼셉트론이 출력하는 신호의 값이 실수형태인데  
그 형태의 값을 정수로 바꿔준다는 말이다.

<br><br>

## Sigmoid function [ 시그모이드 함수 ]

시그모이드 함수라고 불리는 Sigmoid function은 함수를 그리면 S자 형태로 그려진다.  
그래서 Sigmoid function은 Step function보다 매끄럽다는 장점이 있고, 연속적인 실수가 흐른다.
이건 Sigmoid function의 `최대 단점인데 0보다 많이 작으면 0에 엄청 가까워진다.`
이건 나중에 더 자세히 다뤄보도록 하겠다. 


### Code 
```python
def sigmoid_function(x):  
	return 1 / (1 + np.exp(-x))
```

똑같이 x를 퍼셉트론에서 받은 신호의 값이라고 할 때, sigmoid function은 np.exp(-x) 자연상수를 이용해서 계산한다.   
자연상수를 지금 여기서는 다루기도 어려울 것 같고, 그냥 자연상수를 사용한다는 것만 알아두자 

<br><br>

## Relu functioin [ 렐루 함수 ]

랠루 함수라고 불리는 Relu function은 0보다 작거나 같으면 0으로 쭉 가고 0보다 크다면 그냥 자신의 값을 그대로 유지한다.  
Relu function은 그래프를 보면서 이해하면 잘 이해가 되기 때문에 그려서 이해해보자 

### Code 
```python
def relu_function(x):  
	return np.maximum(0, x)
```

Relu function은 위에서 말했던 것 처럼 x가 0보다 작으면 0을 출력하고, 크다면 자신의 값을 그대로 출력한다고 하였다. 
이때 np.maximum을 이용해서 0과 자신의 값을 비교해서 큰 값을 리턴하게 된다.  

<br><br>
# Activate function을 그림으로 그려보자 

## Step
![Step](/assets/img/2023-06-27/Step.png){: width="400" height="400"} 

## Sigmoid 
![Step](/assets/img/2023-06-27/Sigmoid.png){: width="400" height="400"} 

## Relu
![Step](/assets/img/2023-06-27/Relu.png){: width="400" height="400"} 

## 그래프마다 차이점 
![Step](/assets/img/2023-06-27/diff.png){: width="400" height="400"} 

이번 포스팅에는 활성화 함수의 종류와 그래프, 원리에 대해서 조금 알아보았다.  
그럼 활성화 함수 - 2에서는 어떤 활성화 함수가 가장 좋을지 포스팅하도록 하겠다.