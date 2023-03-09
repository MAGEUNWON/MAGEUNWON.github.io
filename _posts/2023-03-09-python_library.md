---
layout: post
title: Python 라이브러리의 이해
tags: [Python]
categories:
  - Python
date: 2023-03-09
---

## 라이브러리란?

라이브러리는 미리 만들어 둔 함수들의 모임으로 import 해서 사용할 수 있음.

라이브러리로 인해서 기능들을 직접 만들지 않고도 필요할 때 이용할 수 있음.

- 라이브러리의 필요성
  - 지수승을 구하고 싶을 때, 라이브러리가 없다면 이런 기능을하는 함수를 직접 만들어야 함

```
import maht

print(math.pow(3, 3)) # 27.0
```

## 라이브러리 설치

라이브러리는 CLI(터미널)에서 명령을 통해 설치할 수 있음.

- 설치 방법 : pip install [라이브러리명]
- 업그레이드 방법 : pip install --upgrade[라이브러리명]

## 라이브러리 사용하기

Python은 math와 같이 기본으로 제공되는 내장 라이브러리가 다수 존재함.

내장 라이브러리는 설치 없이 바로 사용 가능하나, 내장 라이브러리가 아닌 경우 설치해서 사용해야 함

기본 사용법 1 : import [라이브러리명]

```
import math
print(math.factorial(5)) # 120
```

기본 사용법 2: from [라이브러리명] import [함수명]

from을 이용하면 함수명을 import 할 때만 적어주고, 사용할 때는 [라이브러리명] 생략 가능.

```
from math import * # math 라이브러리에 모든 함수를 씀
num = sqrt(5) + factorial(3)
print(num) # 8.23606797749979

from math import sqrt, factorial # math 라이브러리에서 sqrt, factorial 함수만 쓸 때

print(sqrt(5)) # 2.23606797749979
print(factorial(5)) # 120
```

기본 사용법 3: from [라이브러리명] import [함수명] as [바꿀 함수명]

as 구문을 이용하면 라이브러리명이나 함수명을 원하는 이름으로 바꿔 사용할 수 있음.

일반적으로 라이브러리나 함수명이 너무 길거나 직관적인 이름이 필요할 때 변경하여 사용

```
# 라이브러리 이름 바꿔 사용하기
import math as m
print(m.factorial(5)) # 120

# 함수명 바꿔 사용하기
# factorial() 함수를 ff()로 사용 가능
from math iport factorial as ff
print(ff(5)) # 120
```

### 📌 참고 블로그

<br>

[파이썬 라이브러리의 이해](https://velog.io/@jewon119/01.Python-%EA%B8%B0%EC%B4%88-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-%EC%9D%B4%ED%95%B4)
