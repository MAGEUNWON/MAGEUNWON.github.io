---
layout: post
title: Python - 내장 함수
tags: [Python]
categories:
  - Python
date: 2023-03-13
---

# 파이썬 내장 함수

내장 함수는 모듈과 달리 import가 필요하지 않기 때문에 아무 설정 없이 바로 사용할 수 있음.

## abs(number)

숫자를 입력받아 그 수의 절대값을 돌려줌

```
num = -7
print(abs(num)) # 7
```

## divmod(num1, num2)

2개의 숫자를 입력받아, a를 b로 나눈 후 몫과 나머지를 튜플 형태로 돌려 받는 함수

```
print(divmod(7, 3)) #(2, 1)
print(divmod(10, 2)) # (5, 0)
print(divmod(67, 7)) # (12, 3)
```

## dir(object)

dir은 객체가 자체적으로 가지고 있는 변수나 함수를 보여줌

```
print(dir([1, 2, 3])) # ['append', 'count', 'extend', 'index', 'insert', 'pop',...]
print(dir({'1' : 'a'})) # ['clear', 'copy', 'get', 'has_key', 'items', 'keys',...]
```

## eval(string)

실행 가능한 문자열을 입력 받아 문자열을 실행한 결과값을 돌려주는 함수

```
print(eval('1+2)) # 3
print(eval("'hi' + 'a'")) # 'hia'
print(eval('divmod(4, 3)')) # (1, 1)
```

## enumerate(iterable)

반복 가능한 자료형(리스트, 튜플, 문자열)을 입력 받아 인덱스 값을 포함하는 객체를 돌려줌

```
# 리스트에서 활용
for i, name in enumerate(['body', 'foo', 'bar']):
    print(i, name)

# 0 body
# 1 foo
# 2 bar

# 딕셔너리에서 활용
dict_enumerate = {"name":"Tom", "age":10", "location" : "seoul", "birth" : "03-03"}
for i, k in enumerate(dict_enumerate):
    print(i, k)
# 0 name
# 1 age
# 2 location
# 3 birth
```

## all(iterable)

반복 가능한(iterable) 자료형 x를 입력 받아 x의 요소들이 모두 참이면 True, 하나라도 거짓이면 False를 반환  
즉, 하나라도 거짓이면 False, 모두 참일 때만 True

```
a = [1, 2, 3, 4, 5]
b = [1, 2, 0, 4, 5]
c = [False, True, 1, 2, 3]
d = [True, 1, "", 2]
e = [1, 2, "a", True, "false]

print(all(a)) # True
print(all(b)) # False
print(all(c)) # False
print(all(d)) # False
print(all(e)) # True
```

## any(iterable)

반복 가능한(iterable) 자료형 x를 입력 인수로 받은 후 x의 요소들 중 하나라도 참이면 True, 모두 거짓일 때만 False를 반환
즉, 하나라도 참이면 True, 모두 거짓일 때만 False

```
a = [1,2,3,4,5]
b = [1,2,0,4,5]
c = [False, True, 1, 2, 3]
d = [True, 1, "", 2]
e = [1, 2, "a", True, "false"]
print(any(a)) # True
print(any(b)) # True
print(any(c)) # True
print(any(d)) # True
print(any(e)) # True
```

## sorted(iterable)

sorted() 함수는 반복 가능한 데이터에 모두 사용 가능하며, 원본을 수정하지 않음  
또한, sorted() 함수는 입력된 요소를 정렬한 후 결과를 리스트로 돌려줌  
반면, 리스트 자료형에는 sort() 함수는 리스트 자체를 정렬하지만, 결과는 돌려주지 않음.
더불어 sort() 함수는 list에서만 사용 가능

```
iterable_list = [5, 4, 3, 2, 1]
iterable_tuple = ("z", "c", "a", "p")
iterable_dict = {"d":1, "b":20, "k":42}
iterable_str = "4321"

print(sorted(iterable_list)) # [1, 2, 3, 4, 5]
print(sorted(iterable_tuple)) # ['a', 'c', 'p', 'z']
print(sorted(iterable_dict)) # ['b', 'd', 'k', 'u']
print(sorted(iterable_str)) # ['1', '2', '3', '4']
print(iterable_list) # [5, 4, 3, 2, 1]
print(iterable_tuple) # ('z', 'c', 'a', 'p')
print(iterable_dict) # {'d': 1, 'b': 20, 'u': 31, 'k': 42}
print(iterable_str) # 4321

```

## zip(iterable)

요소가 동일한 갯수로 이뤄진 자료형을 묶어 주는 역할을 하는 함수

```
print(list(zip([1, 2, 3], [4, 5, 6]))) # [(1, 4), (2, 5), (3, 6)]
print(list(zip([1, 2, 3], [4, 5, 6], [7, 8, 9]))) # [(1, 4, 7), (2, 5, 8), (3, 6, 9)]
print(list(zip("abc", "def"))) #[('a', 'd'), ('b', 'e'), ('c', 'f')]
```

## filter(fn, iterable)

첫 번째는 함수, 두 번째는 그 함수에 차례로 들어갈 반복 가능한 자료형을 파라미터로 받음.
반복 가능한 자료형 요소가 함수에 순차적으로 입력된 후 함수 내 조건에 해당되는 것들만 걸러서 반환

```
# 일반 함수를 이용했을 때,
# 0보다 큰 숫자만 리턴해주는 함수 기능
def positive(l)
    result = []
    for i in l:
        if i > 0:
            result.append(i)
    retrun result
print(positive(1, -3, 2, -, -5, 6)) #[1, 2, 6]

# 내장함수 filter를 이용했을 때,
# 0보다 큰 숫자만 리턴해주는 함수 기능
def positive(x):
    return x > 0
print(list(filter(positive, [1, -3, 2, 0, -5, 6]))) # [1, 2, 6]

# filter와 lambda 조합 활용 예시
# 0보다 큰 숫자만 리턴해주는 함수 기능
list(filter(lambda x: x > 0, [1, -3, 2, 0, -5, 6])) #[1, 2, 6]
```

## map(fn, iterable)

첫 번째 파라미터인 함수에 두 번째 파라미터인 반복 가능한 자료형의 요소가 순차적으로 입력 됨
순차적으로 입력된 요소가 함수 기능에 따라 적용된 후 반환됨

```
# 함수로 표현 했을 때
def two_times(numberList):
    result = []
    for number in numberList:
        result.append(number*2)
    return result
result = two_times([1, 2, 3, 4])
print(result) # [2, 4, 6, 8]

# 내장함수 map을 사용했을 때,
def two_times(num):
    return num * 2
print(list(map(two_times, [1, 2, 3, 4]))) # [2, 4, 6, 8]

# map과 lambda 조합 활용 예시,,
print(list(map(lambda a: num*2, [1, 2, 3, 4]))) # [2, 4, 6, 8]
```

## isinstance(object, class)

첫 번째 입력받은 객체(인스턴스)가 두 번째 입력받은 class의 인스턴스인지를 판단하여 참이면 True, 거짓이면 False 반환

```
class Person: pass # 클래서 선언
a = Person() # a는 객체이자 Person()의 인스턴스
print(isinsctance(a, Person)) # True
```

## chr(i)

아스키 코드를 입력받아 그 코드에 해당하는 문자를 출력하는 함수

```
print(chr(97)) # 'a'
print(chr(48)) # '0'
```

## hex(int)

정수 값을 입력받아 16진수(hexadecimal)로 변환하여 돌려줌

```
print(hex(234)) # '0xea'
print(hex(3)) # '0x3'
```

### 📌 참고 블로그

<br>

[파이썬 내장 함수](https://velog.io/@jewon119/01.Python-%EA%B8%B0%EC%B4%88-%EB%82%B4%EC%9E%A5-%ED%95%A8%EC%88%98)
