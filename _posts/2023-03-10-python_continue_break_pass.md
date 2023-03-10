---
layout: post
title: Python - continue / break/ pass
tags: [Python]
categories:
  - Python
date: 2023-03-10
---

# continue

- continue는 제어문에서 Body의 반복을 건너띄고 계속 반복을 진행할 수 있게 기능함.
- 즉, 반복문에서 if문을 통해 continue를 만나면 해당 조건을 skip하고 반복문을 계속 진행
- 어떤 반복적인 작업을 수행하다 특정 조건에서만 이를 작동하지 않고 넘어가게 하고 싶을 때 사용

```
for i in range(1, 11):
    if i == 5: continue # 1부터 10까지 반복 중 5를 만나면 skip하고 반복문은 진행
    print(i, end='') # 1, 2, 3, 4, 6, 7, 8, 9, 10
```

# break

- 반복문에서 break에 대한 조건이 일치하면 진행 중인 반복문을 종료하고 빠져나옴
- 반복을 하다 특정 조건을 만나면 반복문을 종료하고 싶을 때 사용

```
for i in range(1, 11):
    if i == 5: break # 1부터 10까지 반복 중 5를 만나면 반복문 종류
    print(i, end '') # 1, 2, 3, 4
```

```
break_list = [7, 4, 3, 2, 6, 5, 9, 1, 8, 10]
n = int(input('1~10 중에서 숫자를 하나 고르세요: '))
for i in break_list:
    print(i, end='')
    if i == n: # 사용자가 입력한 숫자를 만나면 for문 탈출
        break
```

# pass

- 아무 작업도 하지 않음
- 들여쓰기 규칠에 어긋나는 상황(코드 미완성)에서 우선 코드를 오류없이 돌려보기 위해 주로 사용

```
for i in range(1, 11):
    if i == 5:
        pass # 아무작업도 하지 않음
    print(i, end ='') # 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
```

### 📌 참고 블로그

<br>

[파이썬 continue/break/pass](https://velog.io/@jewon119/01.-Python-%EA%B8%B0%EC%B4%88-%EC%A0%9C%EC%96%B4%EB%AC%B8-%EB%B3%B4%EC%B6%A9)
