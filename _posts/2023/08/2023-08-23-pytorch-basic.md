---
title: Pytroch 기초 
date: '2023-08-23 19:02:00 +0900'
categories: [PyTorch]
tags: [PyTorch]
math: true
---

# Pytorch 기초 공부 
## Tensor

### dtype 정수 

```python
a = torch.tensor([1,2,3,4]) # 모두 정수의 값을 가지고 있음 
print(f"a : {a}")
print(f"type : {type(a)}")
print(f"dtype : {a.dtype}")
print(f"shape : {a.shape}")
print()
```
텐서의 선언은 위와 같다.  
`torch.tensor([])` 로 텐서를 선언할 수 있다. 

출력된 결과는 아래와 같다. 

```
a : tensor([1, 2, 3, 4])
type : <class 'torch.Tensor'>
dtype : torch.int64
shape : torch.Size([4])
```

그리고 자세히보면 `dtype`은 int64인것을 확인할 수 있는데 이것은 torch.tesnor([]) 이 안에 모두 정수만 넣었기 때문이다.  
만약 실수가 하나라도 들어가면 dtype은 float으로 바뀐다.  

### dtype 실수

```python
b = torch.tensor([1,2,3.1,4]) 
```
3.1이 하나 들어간 tensor이다.  
dtype을 출력시켜보면 `torch.float32`와 같이 출력된다.  

<br>

## Matrix 
```python
A = torch.tensor([[1,2], [3,4]]) # 행열 선언 
print(A) 
print(A.shape) # 행열의 모양 2x2
print(A.ndim) # 행열의 차원 -> 2차원 
print(A.size()) # 행열의 전체 성분의 수 -> [[2,2]] 
```
텐서를 만들때와 똑같이 만들어주면 된다.  
행열의 차원을 쉽게 알아내는 방법은 `.shape`도 있지만 처음 시작하는 `[`의 갯수를 알아내면 된다.  

- 행열이 몇행 몇열인지 알고싶다면 `.shape`
- 행열의 차원을 알고싶다면 `.ndim`
- 행열의 전체 성분의 수를 알고싶다면 `.size()` 

### 그리고 만약 행열의 `.shape`이 만족하지 않는다면?
```python
B = torch.tensor([[1,2], [3]])
```
```errormessage
ValueError: expected sequence of length 2 at dim 1 (got 1)
```
이렇게 에러메시지가 뜬다.  

<br>

## 텐서의 계산 
### 텐서의 덧셈 
```python
a = torch.tensor([1,2,3])
b = torch.tensor([4,5,6])
print(a + b)
```
각 원소끼리 더한다.

```
tensor([5, 7, 9])
```
[1 + 4, 2 + 5, 3 + 6] = [5, 7, 9]

### 텐서의 뺄셈 
텐서의 뺄셈은 텐서의 덧셈과 원리가 같기에 생략한다.  


### 텐서의 곱셈 
```python
print(a * b)
```
```
tensor([4, 10, 18])
```
텐서의 곱셈은 행열곱셈이 아닌 각 원소에 대한 곱셈이다.  
우리는 이것을 `Hadmard product`라고 부른다.  

`따라서 행열곱이 아니다!!` 진짜 중요하다.  

### 텐서의 행열 곱셈 
이게 진짜 행열 곱셈이다.  
```python
a = torch.tensor([1,2,3])
b = torch.tensor([4,5,6])

A = torch.tensor([[1,2,3], [1,2,3]])
B = torch.tensor([[4,5,6], [1,2,3]])

print(a * b)
print()
print(a @ b) # @ 이 기호가 행열 곱셈 

print(A * B)
print()
print(A @ B)
```
`@` 기호가 행열곱을 의미한다.  
하지만 여기서 행열곱을 한다면 에러가 날 것이다.  
- 왜? 
    - 행열의 사이즈가 맞지 않기 때문이다.  
    - 하지만? 1D tensor라면 에러가 나지 않는다.  
    - 2차원부터 에러가 난다.  

그래서 1D tensor에서는 그냥 행열 몇 by 몇 신경쓰지 말고 행열곱을 해주면 되고,  2차원부터는 신경써줘야 한다.
```
RuntimeError                              Traceback (most recent call last)
Cell In[42], line 13
     11 print(A * B)
     12 print()
---> 13 print(A @ B)

RuntimeError: mat1 and mat2 shapes cannot be multiplied (2x3 and 2x3)
```
보이는 것처럼 1D tensor은 잘 실행이 되는데 2D tensor은 실행이 안된다.  
그래서 이럴때 Transpose()를 해주면 된다.  

```python
print(A @ B.T)

tensor([[32, 14],
        [32, 14]]) 
```
잘 되는 모습!

<br>

## 다양한 함수들 
### 1과 0으로 된 텐서 생성 
```python
print(torch.ones(5)) 
print(torch.zeros(5)) 
print(torch.zeros_like(A)) 

print(torch.arange(3,10,2)) 
print(torch.linspace(0,1,10))  
```
```
tensor([0., 0., 0., 0., 0.])
tensor([[0, 0, 0],
        [0, 0, 0]])

tensor([1., 1., 1., 1., 1.])
tensor([[0., 0., 0.],
        [0., 0., 0.],
        [0., 0., 0.]])

tensor([3, 5, 7, 9])
tensor([0.0000, 0.1111, 0.2222, 0.3333, 0.4444, 0.5556, 0.6667, 0.7778, 0.8889,
        1.0000])
```
- `torch.ones()` : Numpy의 np.ones와 똑같다. 
- `torch.zeros()` : Numpy의 np.zeros와 똑같다. 
- `torch.ones_like()` : Numpy의 np.ones_like()와 똑같다.  
- `torch.arange(3,10,2)` : 3에서 9까지 간격이 2인 텐서를 생성 
- `torch.linspace(0,1,10)` : 0에서 1까지 간격이 일정한 1x10 텐서를 생성


### 난수로 된 텐서 생성 
```python
A = torch.randn(3,3) # 정규분포 
B = torch.rand(3,3)
print(A)
print()
print(B)
```
```
tensor([[-1.0039, -0.9184, -0.9497],
        [-0.0101, -0.2052,  0.7786],
        [ 0.2686, -0.9784,  0.8772]])

tensor([[0.1438, 0.7152, 0.5815],
        [0.3816, 0.8272, 0.2075],
        [0.4899, 0.5709, 0.6862]])
```

- `torch.randn()`
    - 여기서 n은 정규분포의 Normal의 약자이다. 
    - 평균이 0이 된다라는 특징이 있다.  
    - 평균이 0이기 때문에 평균을 5로 만들고 싶다면 `randn() + 5`해주면 된다.

- `torch.rand()`
    - 0 ~ 1사이의 난수를 생성한다.

### 수학과 관련된 함수 
```python
A = torch.randn(3,3)
print(A)

print(torch.abs(A)) 

print(torch.sqrt(torch.abs(A))) 

print(torch.exp(A)) 

print(torch.log(A))
```
```
tensor([[-1.0760, -0.5631, -0.5207],
        [ 0.6822,  0.5903, -0.9017],
        [-0.7448,  0.7442,  0.1061]])

tensor([[1.0760, 0.5631, 0.5207],
        [0.6822, 0.5903, 0.9017],
        [0.7448, 0.7442, 0.1061]])

tensor([[1.0373, 0.7504, 0.7216],
        [0.8260, 0.7683, 0.9496],
        [0.8630, 0.8626, 0.3258]])
```

- `torch.abs` : 절댓값으로 바꿔준다.  
- `torch.sqrt` : 값에 루트를 해준다.
- `torch.exp` : 아 아직 수학을 잘 못한다.. 공식문서에 물어보자..
- `torch.log` : 로그를 취할 수 있다. 
    - 추가로 자주쓰는 log10, log2는 정의가 되어 있다.  
    - log3과 같은 경우에는 내가 따로 정의해줘야함!


- `torch.round()` : 반올림 
- `torch.floor()` : 내림 
- `torch.ceil()` : 올림 

<br>

### 무한? Null? 
- `torch.nan` : not a number 
- `torch.inf` : 무한   

`torch.` 이 뒤에 is라고 붙이면 무한인가?, not a number인가? 가 된다.  

<br>

### 최댓값, 최솟값 
```python 
A = torch.randn(3,4)
print(A)

print(torch.min(A)) # 행열에서 가장 큰 수 

print(torch.max(A, dim=0)) # 행열에서 3x4, dim=0, 행을 기준으로 

print(torch.max(A, dim=1)) # 행열에서 3x4, dim=1, 열을 기준으로  

print(torch.argmax(A))

print(torch.argmax(A, dim=0))
```
```
tensor([[ 0.3054, -1.4724,  0.9370,  1.0452],
        [-0.8061, -0.7421, -0.1098,  1.3403],
        [-0.1578,  0.7950, -1.6094, -1.4934]])

tensor(-1.6094)

torch.return_types.max(
values=tensor([0.3054, 0.7950, 0.9370, 1.3403]),
indices=tensor([0, 2, 0, 1]))

torch.return_types.max(
values=tensor([1.0452, 1.3403, 0.7950]),
indices=tensor([3, 3, 1]))

tensor(7)

tensor([0, 2, 0, 1])
```

-  `torch.min()` : 내가 원하는 텐서나 행열의 최솟값을 알려준다.
    - 뒤에 추가로 `dim`에 대해서 조건을 걸어주면 인덱스와 값을 리턴해준다.

-  `torch.max()` : 내가 원하는 텐서나 행열의 최댓값을 알려준다.
    - min과 동일 

- `torch.argmax()` : 전체 행열중에서 가장 큰 인덱스 번호를 알려준다. 
    - min, max와 동일하게 dim에 대해서 적으면 각각의 인덱스를 리턴 

<br>

### 정렬 
```python
a = torch.randn(6,1)
print(a)
print()
a_sorted = torch.sort(a, dim=0, descending=False)
print(a_sorted)
```
```
tensor([[-0.7293],
        [-0.1292],
        [ 0.0522],
        [ 0.1011],
        [-0.3278],
        [-1.0883]])

torch.return_types.sort(
values=tensor([[-1.0883],
        [-0.7293],
        [-0.3278],
        [-0.1292],
        [ 0.0522],
        [ 0.1011]]),
indices=tensor([[5],
        [0],
        [4],
        [1],
        [2],
        [3]]))
```

- `torch.sort()` : 텐서를 정렬해준다.   
    - `descending = False` : 오름차순 
    - `descending = True` : 내림차순 

<br>

### 차원 유지 
```python
A = torch.randn(3,4)
print(A)
print()
print(torch.sum(A,dim=1)) # 1D array로 나옴
print()
print(torch.sum(A,dim=1,keepdims=True))
```
```
tensor([[ 0.0206, -0.7862, -1.0103, -0.7215],
        [ 0.8947, -0.0662, -1.0131,  0.6161],
        [ 0.2609, -0.4759,  0.0310,  0.2637]])

tensor([-2.4974,  0.4315,  0.0797])

tensor([[-2.4974],
        [ 0.4315],
        [ 0.0797]])
```

만약 내가 행열의 dim=1에 대해서 전부 더하고 이 텐서를 사용하고 싶은데, 차원이 이상하게 나오는 경우가 있다.  
즉, 내가 (3x4)짜리를 넣었다면 출력값은 dim=1에 대해서 (1x3)이 나오는것이다.  
이때 `keepdims=True`라고 적어주면 출력값은 (3x1)이 나온다.  

<br>

### 차원 변경 
```python
A = torch.randint(1,5,size=(12,))
print(A)
print(A.shape)
print()

B = A.reshape(2,2,3)
print(B)
print(B.ndim)
```
```
tensor([4, 3, 1, 2, 2, 2, 4, 4, 4, 2, 4, 1])
torch.Size([12])

tensor([[[4, 3, 1],
         [2, 2, 2]],

        [[4, 4, 4],
         [2, 4, 1]]])
3
```

- `randint(1,5,size=(12,))` : 1,4 사이의 1D tensor 1x12 생성

지금 A.shape은 [12]인데 `.reshape(2,2,3)`을 하면서 B에 넣어준다.  
그러면 2x3이 2개의 채널이 된다.  
- A.reshape(3,4)라고 하면 3x4로 변경 
- A.reshape(3,-1)이라고 하면 3x4로 변경, (-1은 알아서 채워짐)
    - 하지만 (-1,-1)은 안됨 

<br>

### 차원 축소, 확대
#### 축소 
```python
A = torch.randn(1,1,1,3,1,1,4,1)
print(A.shape)
```
```
torch.Size([1, 1, 1, 3, 1, 1, 4, 1])
```

불필요한 차원 1이 들어가있는 차원은 `squeeze()`를 사용해서 축소할 수 있다. 

```python
print(A.squeeze().shape)
```
```
torch.Size([3, 4])
```

#### 확대
반대로 차원을 확대하려면 `unsqueeze()`라고 써주면 된다.
```python
A = torch.randn(3,4)
print(A.unsqueeze(dim=0).shape)
print(A.unsqueeze(dim=1).shape)
print(A.unsqueeze(dim=2).shape)
```
```
torch.Size([1, 3, 4])
torch.Size([3, 1, 4])
torch.Size([3, 4, 1])
```

차원을 확대하는데 dim을 사용해서도 가능하다.  
dim=0이면 dim이 0인 자리에 차원 1이 추가가된다.  
shape을 보면 확인이 가능하다.

<br>

### Transpose 종류 
```python
a = torch.tensor([1,2,3])
b = torch.tensor([2,2,1])

a = a.reshape(3,1)
b = b.reshape(3,1)

# Transpose를 취하는 함수 종류 
print(a.transpose(1,0)@b)
print(a.permute(1,0)@b)
print(a.T@b)
print(a.t()@b)
```

- `a.transpose()` : 괄호안에 자리를 2개까지만 바꿀 수 있음 
- `a.permute()` : 인덱스로 변경 가능 
- `a.T`, `a.t()` : 별거 없고 그냥 transpose 

제일로 좋은건 permute()라고 생각한다.  
- 왜? 
    - 3개 이상으로도 transpose가 가능하니까


<br>

## 행열 쌓기 
### (v, h)stack
```python
A = torch.ones((3,4))
B = torch.zeros((3,4))

C = torch.vstack([A,B]) # (3,4)(3,4) -> (6,4)
D = torch.hstack([A,B]) # (3,4)(3,4) -> (3,8)

print(C)
print()
print(D)
```
```
tensor([[1., 1., 1., 1.],
        [1., 1., 1., 1.],
        [1., 1., 1., 1.],
        [0., 0., 0., 0.],
        [0., 0., 0., 0.],
        [0., 0., 0., 0.]])

tensor([[1., 1., 1., 1., 0., 0., 0., 0.],
        [1., 1., 1., 1., 0., 0., 0., 0.],
        [1., 1., 1., 1., 0., 0., 0., 0.]])
```

- `torch.vstack` : 행열을 세로로 쌓는다. 
- `torch.stack` : 행열을 가로로 쌓는다. 

### cat 
```python
E = torch.cat([A,B], dim=1)
print(E)

E = torch.cat([A,B], dim=0)
print(E)
```
```
tensor([[1., 1., 1., 1., 0., 0., 0., 0.],
        [1., 1., 1., 1., 0., 0., 0., 0.],
        [1., 1., 1., 1., 0., 0., 0., 0.]])
tensor([[1., 1., 1., 1.],
        [1., 1., 1., 1.],
        [1., 1., 1., 1.],
        [0., 0., 0., 0.],
        [0., 0., 0., 0.],
        [0., 0., 0., 0.]])
```

- `torch.cat` : vstack, hstack와 기능은 같지만 dim에 대해서 가능하다.  

실제로 3차원 이상부터는 vstack, hstac은 잘 안쓴다고 한다.  
솔직히 알아보기 너무 어렵다.  