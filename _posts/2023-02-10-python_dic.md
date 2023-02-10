---
layout: post
title: Python 딕셔너리(dictionary)
tags: [Python]
categories:
  - Python
date: 2023-02-10
---

## 파이썬 딕셔너리(dictionary)

<br>

'딕셔너리'라는 이름은 파이썬의 큰 특징. 데이터를 다루는 관점에선 엄격한 작성구분이 상당히 편리한 장점으로 활용됨. 파이썬이 데이터에 강한 면모를 보이는 시작점은 바로 엄격한 데이터 타입 지원에 있음. 객체를 여러가지로 구분하는 관점을 챙길 것!

```
#파이썬은 자바스크립트에서 부르는 객체(object)의 형태를
#사전이란 뜻의 딕셔너리(dictionary), 약칭 dict라고 부름

pokemon = {"id_value" : 1, "name" : "이상해씨", "type_value" : "풀"}

#"id_value 는 키(key)
#1 은 값(value)
#딕셔너리 자료형은 키와 값의 쌍으로 이루어짐


print(pokemon["id_value"])
print(pokemon["name"])
print(pokemon["type_value"])

```

- 특이한 점은 키(key)에 해당하는 property 부분을 "문자열(string)"로 명시한 점을 눈여겨 볼 필요가 있음 마치 JSON 파일 포멧팅 형식과 닮았음

- dictionary의 속성값을 접근하는 방식은 자바스크립트와 달리 [] 대괄호 표기법을 기본으로 하고 있음

- 자바스크립트는 점표기법, 대괄호표기법 두개를 병용할 수 있는 것과 달리 파이썬은 명확하게 딕셔너리 타입 일 때, 생성자 함수(class)일 때를 구분 함.

- 이 부분에 대한 표기 방식이 자바스크립트보다 엄격하기 때문에 object의 시작점 형태를 수월하게 파악할 수 있는 장점이 있음

### 딕셔너리에 특정 키 있는지 확인하기

```
pokemon = {"id_value" : 1, "name" : "이상해씨", "type_value" : "풀"}

'id_value' in pokemon
#True

'skill' in pokemon
#False
```

딕셔너리에 어떤 키가 있는지 없는지는 in을 써서 알아 볼 수 있음! 있으면 Ture, 없으면 Flase라고 대답해줌~!

### 📌 참고 블로그

<br>

[파이썬 딕셔너리](https://wikidocs.net/72)
