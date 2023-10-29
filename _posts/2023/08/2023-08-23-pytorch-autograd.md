---
title: Pytroch Autograd
date: '2023-08-23 23:11:00 +0900'
categories: [2. Machine Learning & DeepLearning, 2 - 2 Pytorch 튜토리얼]
tags: [PyTorch]
math: true
---

# Pytorch 기초 공부 

## Autograd란?
- `pytorch.autograd` 란 자동 미분 엔진이다.  

자동미분 엔진? 이게 무슨 말일까..  

딥러닝에서는 backward()라는것을 한다. 우리는 이를 `오차역전파`라고 부른다.  
오차역전파는 뒤에서 앞으로 값을 미분하면서 앞으로 보내게된다.  
오차역전파에 대한 설명은 생략하도록 하고 어쨌든 이럴때 미분해야하는 일이 생긴다.  

그때 autograd를 사용한다.  

<br>

## 어떻게 사용해? 
autograd는 일단 미분을 뒤에서 앞으로 하기 때문에 `추적`이라는게 되어야한다.  
- 왜? 
    - 추적이 되지 않는다면 어디에서 미분을 해서 어떻게 앞으로 보낼꺼지?? 

그래서 torch.autograd를 사용할 변수에는 특별하게 한 가지를 넣어줘야한다.  

`requires_grad=True`이다.  

선언해보자  

```python
import torch 

x = torch.tensor([1], requires_grad=True)
```
```
RuntimeError: Only Tensors of floating point and complex dtype can require gradients
```

- 왜 에러가 나는걸까?  
    - 생각해보자 상수를 미분한다? -> 상수를 미분하면 0이다! 

따라서 실수값을 적어줘야한다.  
위에서는 [1]이라고 주었지만 이제는 실수값 [1.]로 준다.  

- 1.0과 1. 은 서로 같은 것 이다.
  

이제 값을 수정하고 다시 실행해보면 
```python
print(x)
```
``` 
tensor([1.], requires_grad=True)
```
이렇게 `requires_grad=True`가 잘 뜨는 모습이다.  
이 뜻은 `이 변수를 추적한다` 라고 생각하자  

- 근데 requires_grad=False면? 
    - 그냥 tesnor([1.])이라고 출력된다.  


<br>

## autograd 맛보기 
진짜 정말 간단하게 아래 식을 미분해보자.  

$$y = x^2$$

위 식을 미분하면???  

$$y = 2x$$ 

자 이것을 코드로 나타내보자  

```python
x = torch.tensor([1.], requires_grad=True)
y = x**2
print(y)
```
```
tensor([1.], grad_fn=<PowBackward0>)
```

잉 1.은 알겠는데 저 뒤에 뜨는건 뭘까?  
- Pow는 제곱이라는 뜻이다.  
- 맨 마지막으로 계산한 식이 x**2이기 때문에 제곱인 Pow가 찍히는 것이다.  

자 그럼 이제 내가 미분하고 싶은 변수의 뒤에 `.backward()`라고 적어주기만 하면 미분이 된다.  

```python
y.backward()
print(x.grad)
```
```
tensor([2.])
```

자 위의 값이 어떻게 나오는지 차례대로 짚어보자.  

- 1. 추적이 가능한 변수를 생성한다 -> x
- 2. x와 관련된 식 (예시로 y=x**2)을 정의한다. 
- 3. y를 미분하기 위해서 y.backward()라는 코드를 실행한다. 
- 4. x.grad라는 것을 사용해서 출력시키면 미분된 값에 x를 대입한 결과가 출력된다.  

`.grad`라는 것은 requires_grad=True인 변수에만 사용이 가능하다.  
혹시나 더 궁금하다면 공식문서를 찾아보자  

<br>

### .grad를 미분하기 전에 한다면? 
미분을 하기 전에 .grad를 사용하게 된다면 값이 None라고 뜬다.  
이유는 backward()를 해야 .grad에 값이 담기게 되는데 그 전에 출력을 해버리면 빈 값이기 때문이다.  

<br>

## 하나의 식을 더 추가해보자 

$$x = 1$$
$$y = x^2$$
$$z = 3y$$

이렇게 있다고 하고 코드로 작성해보자 

```python
x = torch.tensor([1.], requires_grad=True)
y = x**2
z = 3*y

z.backward()

print(x.grad)
print(y.grad)
```
```
tensor([6.])
None
```

$$\frac{∂z}{∂x} = \frac{∂z}{∂y} \frac{∂y}{∂x} = \frac{3x^2}{x^2}\frac{x^2}{x} = 3x * 2 = 6x$$

따라서 x에 1을 대입하면 6이 되는것이며, y.grad가 None가 뜨는 이유는 잘 모르겠어서 GPT한테 물어봤는데  
"여기서 y가 이미 그래디언트를 계산하는 연산의 결과로서 사용되었기 때문에, 그래디언트 계산은 더 이상의 역전파가 필요하지 않습니다."  

라고 말해줬는데 이게 맞는지 아닌지는 잘 모르겠다.  
그래서 이 부분은 구글링을 조금 더 해보도록 하겠다.  

<br>

## requires_grad=True인 식이 2개? 

처음 설명에서는 requires_grad=True인 변수가 1개였다.  
그래서 이번에는 총 2개로 늘리고 잘 되는지 확인해보겠다.  

```python
x = torch.tensor([1.], requires_grad=True)
y = torch.tensor([1.], requires_grad=True)
z = 2*x**2 + y**2
z.backward()

print(x.grad)
print(y.grad)
```
```
tensor([4.])
tensor([2.])
```

앞에서 원리는 설명한거같으니 이번에는 그냥 말로하겠다.  
z를 미분하면 $4x + 2y$가 된다.  

그리고 x=1을 z에 대입, y=1을 z에 대입하면 4.,2.라는 값이 각각 나온다.  
따라서 출력이 4., 2.이 되는것이다.

<br>

## 왜 requires_grad=False는 안될까?
transfer learning같은 것들을 돌릴때는 False로 해야한다.  
True는 학습을 시킬때와 비슷한 상황에만 사용한다.  

또 다른건 어떤것이 있을까? 

- `x.detach()` : 변수 x에 대해서 requires_grad를 False한다.  

- `torch.no_grad():` 이것은 if문 처럼 사용이 가능하다. 
    - 이것을 사용하면 실제로는 False가 되지 않고 그 영역에서만 임시로 False가 되어서 코드가 돌아간다.  

사용 예시) 
```python
with torch.no_grad():
    이건 코드입니다.
    저것도 코드입니다.
    a = 10
    블라블라 
```

