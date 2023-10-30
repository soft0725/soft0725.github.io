---
title: C++ - Hello World!
date: '2023-10-30 16:06:00 +0900'
categories: [1. Software, 1 - 1 C++]
tags: [C++, Programming]
---

# Hello World!

```cpp
#include <iostream>

using namespace std;

int main()
{
    cout << "Hello World!";

    return 0;
}
```

모든 언어들의 시작은 Hello World부터 시작한다.  

일단 위 코드를 한 번 뜯어보자 

## using namespace std

이 부분은 std라는 클래스를 불러오는 것과 같다.

즉, using namespace std가 없다면, 아래와 같이 써야한다. 

```cpp
std::cout << "hello"
```

딱히 없어도 상관은 없지만 cout 를 사용할 때마다 std::를 사용하기 싫으니 붙이도록 하자…

## 출력, 입력?

C++에서는 입력과 출력은 다음과 같다. 

`cout` : 출력 

`cin` : 입력 

# 입력

위에서는 간단하게 Hello World를 출력하는 코드를 짜보았다. 

그럼 이제 입력도 한 번 해보자 

```cpp
#include <iostream>

using namespace std; 

int main()
{
    int a;
    cin >> a; 

    cout << a;

    return 0;
}
```

코드는 다음과 같다. 

1. 정수형 a를 선언한다. 
2. cin >> 을 통해서 a를 입력 받는다. 
3. cout << 를 통해서 a를 출력한다.