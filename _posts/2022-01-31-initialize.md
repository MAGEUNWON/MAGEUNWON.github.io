---
layout: post
# permalink: /study/
title: 자바스크립트 =, ==, ===의 차이와 초기화
tags: [javascript, js]
categories:
  - javascript
date: 2023-01-31
---

### 자바스크립트 =, ==, === 연산자의 차이

= : 자바스크립트에서 = 는 같다는 의미가 아니라 대입한다는 뜻. 대입 연산자

== : 동등(coercive) 연산자. 값을 비교해줌. 값이 일치하면 true, 일치하지 않으면 false를 반환. 값을 비교하기 전에 강제 형 변환(Type Coercion)를 수행. 강제 형변환 과정을 통해 피연산자들을 공통 타입으로 만들고 그 안에 있는 값만 비교하는 <mark>느슨한 비교를</mark> 함.

```
a = a // true
10 = '10' //true
true == 1 //true. 두 피연산자에서 불리언 값이 존재하면 불리언 값을 1로 변환 후 값을 비교함.
true == '1' //true
true == 'true' //false 불리언 값을 1로 변환해도 문자열 true느 숫자로 변환 불가하므로 false
null == undifinde //true. null과 undifined는 엄연히 다르지만, ==연산자에서는 true를 반환함.
```

=== : 일치(stirc) 연산자. 값을 비교해줌. 강제 형변환 과정을 수행하지 않는 <mark>엄격한 비교</mark>를 함. 값이 같아도 타입이 다르면 false를 반환함.

```
10 === 10 //ture
10 === '10' //false
true === 1 //false
ture === 'ture' //flase
null === undifined //flase
NaN === NaN //flase
```

- NaN 값은 자기 자신을 포함하여 어떠한 값과도 일치하지 않음. === 연산자에 NaN 값이 존재하는 경우 항상 false임.

### 초기화

개발에서 초기화란 처음 설정, 혹은 최초 설정을 의미함.  
init 혹은 initialize라고 쓰여져 있다면 무언가 핵심으로 다루는 키(key)일 확률이 높음.

- 초기화(initialize) : 변수선언과 동시에 값이 할당(원래로 돌아갔다는 통상적인 의미보다 "초기설정"의 의미를 가짐)

- 변수 선언

```
let a = 1;
```

let(variable, 변수) -> 변수를 선언하는 약속 let. 변수 선언자라고 부르기도 함.

a(operand, 피연산자) : 변수명. 변수 이름은 개발자가 작명하면 됨.

1 : 데이터 타입이 숫자인 '값(value)' 1임

;(세미콜론) :세미콜론은 자바스크립트에서 작성이 끝났음을 의미. 한글에서 마침표(.) 와 같은 역할
