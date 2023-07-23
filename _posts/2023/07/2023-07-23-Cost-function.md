---
title: Cost function
date: '2023-07-23 16:42:00 +0900'
categories: [DeepLearning, 원리]
tags: [구현]
math: True
---

# Cost function 구현, 종류 

Cost function은 Linear regression에서 평가할 때 주로 사용되며 종류가 다양하다.  
MSE, RMSE, MAE... 등 정말 많지만 이 글에서는 앞에 말했던 3 가지만 정리해보도록 하겠다.  

<br>

## MSE 
MSE는 Mean squared error로 `평균 제곱 오차` 라고 부르며 가장 대표적으로 쓰인다.  

### 원리 
MSE는 실제 값에서 가설을 뺸 다음 제곱해서 다 더한 뒤 평균을 낸다.  
- 식

$$ MSE = \frac{1}{n} \sum_{i=1}^{n} (y - \hat{y})^2 $$
<br>

- 설명 
    - $y$ : 실제값, $\hat{y}$ : 가설  

    - $y -  \hat{y}$ 를 계산한다음 제곱하고 그 값을 전부 더한다.

    - 만약 데이터가 100개라면 100개의 `SE`를 구한 뒤 전부 더하는 것이다. 

    - 마지막으로 다 더한 값을 데이터의 갯수만큼 나눠주면 된다.  

위에서 SE는 Mean이 들어가지 않은 그냥 하나의 Squared error을 말한다.  
만약 Mean이 있다면 전체의, 없다면 하나의 라고 생각하면 될 것 같다.  

### 구현 

```python
def MSE(x, y):
    loss = 0
    
    for i in range(len(x)):
        loss += (x[i] - y[i]) ** 2 
        
    return loss / len(x)
```

MSE는 위와 같은 코드로 구현할 수 있다.  

`for i in range(len(x))`는 모든 데이터의 SE를 구해야하기 때문에 len(x) 즉 데이터의 갯수만큼 반복하고  
안에서 `loss`라는 변수에 $(y - \hat{y})^2$을 계산한 결과를 더한다.  
그러면 모든 데이터에 대한 SE의 총 합이 loss라는 변수에 담기게 되는데 이때  
return하는 값을 데이터의 갯수만큼 나눠준다면 MSE를 구할 수 있다.  

<br><br>



## RMSE 
RMSE는 Root mean squared error로 `평균 제곱근 오차` 라고 부른다.  
그냥 MSE에 루트를 씌운것이다.

### 원리 
RMSE는 MSE에 그냥 루트 하나만 씌어주면 된다.  
원리는 MSE와 동일하고 그냥 루트만 더해졌다고 생각하면 된다.
- 식

$$ RMSE = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y - \hat{y})^2} $$
<br>

- 설명 

    - MSE에 루트를 씌움 

### 구현 

```python
import math

def RMSE(x, y):
    loss = 0
    
    for i in range(len(x)):
        loss += (x[i] - y[i]) ** 2 
        
    return math.sqrt(loss / len(x))
```

RMSE는 MSE 코드에서 리턴하는 값을 루트 씌워준게 끝이다.

<br><br>

## MAE 
MAE는 Mean absolute error로 `평균 절댓 오차` 라고 부른다.  
MSE와는 반대로 제곱이 아닌 절댓값의 형태를 취해준 것이다.

### 원리 
MSE의 원리에서 제곱이 사라지고 절댓값이 생겼다고 생각하면 된다.

- 식

$$ MAE = \frac{1}{n} \sum_{i=1}^{n} \left\vert (y - \hat{y}) \right\vert $$ 


- 설명 

    - MSE 에서 제곱이 사라지고 절댓값이 생겼다.

### 구현 
```python
import math

def MAE(x, y):
    loss = 0
    
    for i in range(len(x)):
        loss += abs(x[i] - y[i]) 
        
    return loss / len(x)
```
abs를 사용해서 절댓값을 취한 뒤 loss에 더해주었다.  
그것말고는 MSE와 다를게 없다.

<br><br>
