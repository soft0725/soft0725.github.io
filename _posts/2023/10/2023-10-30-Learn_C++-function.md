---
title: C++ - 함수
date: '2023-10-30 17:42:00 +0900'
categories: [1. Software, 1 - 1 C++]
tags: [C++, Programming]
---

# 함수의 두 가지 종류

## 1. 짧게 쓰는 함수

```cpp
#include <iostream>

using namespace std;

int sum(int a, int b){return a + b;};

int main()
{
    int a, b, result;
    cin >> a;
    cin >> b; 
    result = sum(a, b);

    cout << result;

    return 0;
}
```

위 함수는 `sum(int a, int b){return a + b;};` 이렇게 짧게 쓴 함수이다.  

처음 a와 b를 입력받아서 sum이라는 함수로 a와 b의 합을 리턴받고 출력하는 함수이다.

## 2. 일반 함수

```cpp
#include <iostream>

using namespace std;

void isOne(int a)
{
    if(a == 1)
    {
        cout << "One";
    }
    else
    {
        cout << "Not Thing";
    }
}

int main()
{
    int a;

    cin >> a;

    isOne(a);

    return 0;
}
```

위 코드는 `void isOne()` 이라는 함수를 만들어보았다. 

동작원리는 아래와 같다

1. a를 입력받고 a가 1이라면 One 출력 
2. 아니라면 Not Thing을 출력하는 코드이다. 

<br>

## 두 함수의 차이점

- 일단 가장 큰 차이점은 코드의 길이 일 것이다.
    - 코드가 길면 길수록 좋을수도 있지만 두 변수의 값을 합하는 함수는 짧게쓰는 것이 좋다.
- 자료형이 다르다
    - void는 값을 리턴하지 않는다.
    

# 오버로딩

```cpp
#include <iostream>

using namespace std; 

int print(int a)
{
    cout << a << endl;
}

float print(float b)
{
    cout << b << endl;
}

int main()
{   
    int a;
    float b;
    
    a = 3;
    b = 3.1;

    print(a);
    print(b);

    return 0;
}
```

C++에서는 함수의 이름이 자료형만 다르다면 똑같이 사용할 수 있다. 

# 함수 템플릿

```cpp
#include <iostream>

using namespace std; 

template <class Any>
Any sum(Any a, Any b)
{
    return a + b;
}

int main()
{
    int a, b, result1;
    a = 3, b = 5;
    result1 = sum(a, b);

    cout << "값 : " << result1 << ", 자료형 : " << sizeof result1 << endl;

    double c, d, result2;
    c = 3.5, d = 5.5;
    result2 = sum(c, d);

    cout << "값 : " << result2 << ", 자료형 : " << sizeof result2 << endl;

    return 0;
}
```

위 함수는 `Any` 를 사용한 함수이다. 

## Any란?

위 코드를 잘 보면 알겠지만, 아래 전달되는 변수의 자료형에 따라서 Any가 정해진다.

즉, a와 b가 int라고 하면 sum이라는 함수를 호출 했을 때 Any는 int가 되게 된다.

출력도 보면 

```cpp
값 : 8, 자료형 : 4
값 : 9, 자료형 : 8
```

이렇게 나오면서 확실히 함수의 자료형이 바뀌고 있는 것을 알 수 있다.