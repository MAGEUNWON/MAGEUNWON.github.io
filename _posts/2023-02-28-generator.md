---
layout: post
title: Python 제너레이터(Generator)
tags: [Python]
categories:
  - Python
date: 2023-02-28
---

## 제너레이터란?

제너레이터는 "이터레이터(Iterator)를 생성하는 객체라고 할 수 있음.

- 제너레이터는 이 객체를 호출할 때마다 yeild가 작동되어 값을 순차적으로 산출함.

- 함수 내부에서 yield가 사용되면 그 함수는 제너레이터가 되며, 제너레이터는 이터레이터를 생성해 줌.

- 이터레이터는 클래스에 iter, next 등의 메서드를 구현해야 하지만 제너레이터는 함수 안에서 yeild라는 키워드만 사용하면 손쉽게 생성할 수 있다는 장점이 있음.

- yield로 생성된 제너레이터는 이미 iter와 next를 갖고 있는 것을 아래와 같이 확인할 수 있음.

```
def generator_func():
    yield 1
    yield 2
    yield 3
print(generator_func()) # <generator object generator_func at 0x7fc786582580>
print(hasattr(generator_func(), '__iter__')) # True
print(hasattr(generator_func(), '__next__)) # True
```

yield는 오른쪽 값을 함수 밖으로 산출(생산해서 반환하고), 실행을 양보함.

- yield로 생성한 함수는 제너레이터를 반환하기 때문에 iter를 사용할 필요 없이 바로 next로 yield 오른쪽에 위치함 값을 순차적으로 함수 밖으로 산출해 줌

- 함수 return과 제너레이터의 yield의 차이점은 return은 함수가 호출되면 값을 반환하고 함수를 종료시키지만, yield 함수 내부에서 함수 외부로 값을 순차적으로 전달해 준다는 점임. 뿐만 아니라 send 함수를 통해 mianroutine에서 값을 받아와 양방향 통신도 할 수 있음.

- 즉, 제너레이터는 제너레이터의 객체(함수)가 호출되었을 때, yield 오른쪽의 값을 반환하고 바로 다음 yield의 위치를 기억한 상태로 다음 제너레이터 호출(실행 양보)을 기다림.

```
def generator_func():
    yield 1
    yield 2
    yield 3

g = generator_func() # yield를 통해 생성된 제너레이터

print(g)  # <generator object generator_func at 0x7fc786582580>
print(g.__next__()) # 1
print(g.__next__()) # 2
print(g.__next__()) # 3
```

## 제너레이터 함수

제너레이터 함수를 쉽게 설명하면 return 키워드 대신 yield라는 키워드를 사용하는 함수임. return 이라는 키워드는 결괏값을 돌려주고 함수도 끝나버리지만 yield라는 키워드는 결괏값을 돌려주지만 실행의 상태를 그대로 저장해 둔채로 잠시 멈추는 것. 따라서 나중에 다시 이전에 멈춘 상태에서부터 이어서 다음 코드를 실행할 수 있게 됨.

아래 코드는 num_gen 안에 yeild라는 키워드가 사용됨

```
def num_get():
    for i in range(3):
        yield i

g = num_gen()  # 제너레이터 객체 생성

num1 = next(g)
num2 = next(g)
num3 = next(g)

print(num1, num2, num3)
```

yield가 사용된 함수는 ()를 붙여도 코드가 바로 실행되지 않음. 대신 제너레이터라는 객체가 생성되고 코드가 실행될 준비를 함. 제너렝리터 객체를 생성했다면 next() 함수 호출을 통해 제너레이터 객체 내의 코드를 실행할 수 있는데 이때 yield 구문을 만나면 파이썬 함수의 return 처럼 yield 키워드에 있는 값(여기서는 i)을 호출부로 리턴하고 실행의 흐름도 호출부로 이동하게 됨. 다만 파이썬 함수와 달리 현재 상태를 그대로 유지할 수 있음. 코드가 중지된 시점의 상태를 유지하고 있기 때문에 해당 상태로부터 다시 코드를 이어서 실행할 수 있음.

다시 호출부에서 next() 함수를 호출하면 앞서 제너레이터의 중지된 상태에서부터 코드가 실행됨. 이전에 for문에서 i가 0일 때를 실행하고 멈ㅊㄴ상태 이므로 i는 1을 바인딩한 후 다 yield 1 구문까지 코드가 실행 됨.

## for와 제너레이터 함수

제너레이터 함수를 호출하면 다음과 같이 generator클래스의 객체가 생성됨

```
def num_gen():
    for i in range(3):
        yield i

g = num_gen()
print(g, type(g))
```

g 변수가 바인딩하는 제너레이터 객체는 next(g)를 호출할 때 0, 1, 2 라는 값을 순서대로 돌려줌. 이 때 한번 더 next(g)를 호출하면 더이상 돌려줄 값이 없기 때문에 StopIteration이라는 에러가 발생

```
def num_gen():
    for i in range(3):
        yield i

g = num_gen()
print(next(g))
print(next(g))
print(next(g))
print(next(g))
```

```
Traceback (most recent call last):
  File "/Users/brayden/PycharmProjects/study/mygen.py", line 9, in <module>
    print(next(g))
StopIteration
0
1
2
```

next(g)를 사용하지 않고 제너레이터로부터 값을 가져오는 더 쉬운 방법은 for문을 사용하는 것. for문을 사용하면 반복할 때마다 내부적으로 next(g)를 호출하는데 이는 StopIteration이 발생할 때 까지 계속 됨. 즉, 다음과 같이 코딩하면 알아서 제너레이터 객체로부터 순차적으로 값을 가져오게 됨

```
def num_gen():
    for i in range(3):
        yield i

g = num_get()

for i in g:
    print(i)
```

출력값은 다음과 같이 yield 키워드를 통해 리턴하는 값이 출력됨을 확인 할 수 있음.

```
1
2
3
```

## 제너레이터를 사용하는 이유

제너레이터로 이터레이터를 만들지 않으면, 선언과 동시에 메모리를 소모시킴. 데이터 양이 많아졌을 때 아래와 같은 코드는 메모리 효율성이 좋지 않음.

예시1

```
numbers = [i for i in range(10)]
print(numbers) # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

예시2

```
def 빵만들기(n):
    빵쟁반 = []
    for i in range(n):
        빵 = "빵" + str(i)        # 빵0, 빵1, ..., 빵99
        빵쟁반.append(빵)
    return 빵쟁반


def 빵포장(빵):
    print("{} 포장완료".format(빵))


for i in 빵만들기(100):
    빵포장(i)
```

이에 제너레이터를 통해 이터레이터를 생성하면 다음 순서를 기억한 상태로 객체가 생성되고, 호출하기 전에는 모든 값을 메모리에 올리지 않음. 즉, yield를 호출해 generator를 가동시키므로써 값을 산출하고 그만큼의 메모리를 사용함.

이를 지연 평가(lazy evaluation) 방식이라고 함.

제너레이터를 통해 이터레이터를 만들면 다음과 같음.

예시1

```
def numbers():
    yield 0
    yield 1
    yield 2
    yield 3
    yield 4
    yield 5
    yield 6
    yield 7
    yield 8
    yield 9
gen_numbers = numbers() # 제너레이터로 이터레이터 생성
print(gen_numbers) # <generator object numbers at 0x7fcb396199e0>
for i in gen_numbers:
    print(i, end=" ") # 0 1 2 3 4 5 6 7 8 9
```

예시2

```
def 빵만들기(n):
    for i in range(n):
        빵 = "빵" + str(i)        # 빵0, 빵1, ..., 빵99
        yield 빵

def 빵포장(빵):
    print("{} 포장완료".format(빵))

for i in 빵만들기(100):
    빵포장(i)
```

## yield from

yield로 이터러블한 객체의 요소를 하나씩 리턴해 줄 수도 있음. 이 경우 yield에 더해 from이라는 키워드를 사용하면 됨

```
def func():
    _list = [1, 2, 3, 4, 5]
    for i in _list:
        yield i
```

위와 같이 리스트를 순회하며 각각 값을 yield로 반환하는 대신

```
def func():
    _list = [1, 2, 3, 4, 5]
    yield from _list
```

이렇게 for문 없이 yield로 반환하는 것도 가능.

추가로 이렇게 yield from 키워드로 제너레이터를 전달하는 것도 가능함. 10 이하의 짝수를 foo 객체에서 next로 하나씩 꺼내올 수 있음.

```
def generator(stop_number):
    num = 0
    while True:
        if num >= stop_number:
            return
        num +=2
        yield num

def func(stop_number):
    gen = generator(stop_number)
    yield from gen

foo = func(10)
```

### 📌 참고 블로그

<br>

[파이썬 제너레이터](https://wikidocs.net/83132)

[파이썬 제너레이터 개념정리](https://velog.io/@jewon119/TIL30.-Python-%EC%A0%9C%EB%84%88%EB%A0%88%EC%9D%B4%ED%84%B0Generator-%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC)

[파이썬 제너레이터란?](https://tibetsandfox.tistory.com/28)
