---
title: Cost function과 Loss function의 차이점은 무엇일까?
date: 2023-06-29 23:46:00 +0900
categories: [딥러닝 공부]
tags: [비용 함수, 손실 함수]
---

  

# Loss function ( 손실 함수 )

`손실 함수`는 하나의 데이터와 예측한 가설의 오차를 계산하는 함수이다.

예를 들어서 하나의 데이터에서 가설까지 수직으로 이었을때의 값을 말하는 것이다.

표로 나타내서 보여주겠다.

  
  

```python
import numpy as np
import matplotlib.pyplot as plt
```


```python
x = [1, 2, 3, 4, 5]
y = [1, 2, 3, 4, 5]

plt.figure(figsize=(3, 3))
plt.plot(x, y)
plt.show()
```

  
  

![png](/assets/img/2023-06-29/output_3_0.png)

  
  

`y = x`인 그래프를 그렸다.

  
  

```python
data_x = [3]
data_y = [4]

plt.figure(figsize=(3, 3))
plt.scatter(data_x, data_y, color = 'red')
plt.plot(x, y)
plt.show()
```

  
  

![png](/assets/img/2023-06-29/output_5_0.png)

  
  

무수히 수많은 데이터가 있지만 보이지 않는다고 가정하고, `단 하나의 데이터를 빨간색 점이라고 할 때`
저 빨간색 데이터에서 가설(파란색 선) 까지의 거리까지의 오차값을 구하는 것이 손실 함수이다.

예시로 MSE에 대해서 나타내 보겠다.

  

**SE(제곱 오차) :** $(\hat{y} - y)^2$

  

하나의 데이터에서만 오차값을 계산하기 때문에 MSE와는 다른점이 M이 빠졌다는 점이다.

  

그럼 저 빨간 점에 대해서 오차값을 계산하면 (3,3)에서 수직으로 그은 직선 값이 된다.

  
  

```python
Error = (data_y[0] - 3)**2

print(f'빨간 데이터에 대한 오차값 : {Error}')
```

  

빨간 데이터에 대한 오차값 : 1

  
  

# 비용 함수

  

그럼 반대로 cost function 비용 함수는 `모든 데이터들의 평균 오차값을 계산하는 함수이다.` 말 그대로 손실 함수와는 다르게 모든 데이터에 대해서 오차값을 낸다는 것이다.

이것도 코드로 보자

  
  

```python
data_x = [1, 2, 3, 4]
data_y = [2, 3, 4, 5]

plt.figure(figsize=(3, 3))
plt.scatter(data_x, data_y, color = 'red')
plt.plot(x, y)
plt.show()
```

  
  

![png](/assets/img/2023-06-29/output_13_0.png)

  
  

위 처럼 있다면 4개의 데이터에 대해서 모든 오차값을 더해서 평균으로 낸다는 것이다.

이것을 `MSE` 방식으로 나타내보겠다.

__(그냥 간단하게 y값이 1만 차이가 나도록 설정하겠다.)__

  
  

```python
Error = 0

for i in range(len(data_x)):
    Error += (data_y[i] - y[i])**2 # (y^ - y)^2을 모두 더함
    print(Error)

print(f'MSE에 대한 오차값 : {Error / len(data_x)}') # 마지막에 데이터 n개 만큼 나눠줌
```

  

>1  
2  
3  
4    
MSE : 1.0

  
  

MSE를 수식으로 나타내면  

![png](/assets/img/2023-06-29/MSE.png)
  
가 되기 때문에 위에 식에서 전부 더한 뒤에 마지막에 나눠준 모습을 확인할 수 있다.


나는 이제 비용 함수와 손실 함수의 차이점에 대해서 잘 알게된거 같아서 행복하다. ㅎㅎ