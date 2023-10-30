---
title: C++ - Struct!
date: '2023-10-30 18:24:00 +0900'
categories: [1. Software, 1 - 1 C++]
tags: [C++, Programming]
---

# 구조체

```cpp
#include <iostream>

using namespace std; 

struct Player
{
    int age;
    char Name[10];
    char TeamName[20];
};

int main()
{
    Player A = {
        10,
        "chan",
        "BSSM"
    } ;

    cout << A.age << endl; 
    cout << A.Name << endl;
    cout << A.TeamName << endl;

    return 0;
}
```

struct player를 생성한다. 

이때 구조체의 이름은 player이 된다. 

- 메인함수에서 A라는 변수에 정보를 기입한다.
- 그러면 변수.구조체변수이름 으로 출력할 수 있다.