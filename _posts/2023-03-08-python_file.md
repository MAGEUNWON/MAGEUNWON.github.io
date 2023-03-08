---
layout: post
title: Python 파일 읽고 쓰기
tags: [Python]
categories:
  - Python
date: 2023-03-08
---

# 파일 다루기

- 파이썬에서 다루는 파일의 형식들은 다양함
- 일반 텍스트 파일, CSV 파일, JSON 파일, YAML 파일, EXCEL 파일, PDF 파일, Image 파일 등
- 파일에서 데이터를 읽어들여 처리하거나, 결과물을 파일로 남기기도 함.

## 파일 생성하기

### open() 함수

- 파일을 다룰 때, open() 함수를 사용하면 파일을 생성해주고, 기존에 있던 파일이면 해당 파일을 다룰 수 있도록 열어 줌.

- open() 함수는 여러가지 파라미터(경로, 모드, 인코딩 등)를 가지고 있음.

- 'w' 모드는 write의 약자로 파일을 생성할 때 쓰임

  - r : 읽기 모드(파일을 불러올 때 사용)
  - w : 쓰기 모드(파일에 내용을 작성할 때 사용)
  - a : 추가 모드(이미 작성된 내용은 유지하고 뒷 부분에 추가 시킬 때 사용)

- 인코딩은 디폴트 값으로 'cp932'이 정의되어 있고, 한국어나 중국어와 같은 언어를 읽고 쓰려면 'utf8'을 인코딩 값으로 넣어줘야 함

- f = open("파일이름.txt, 'w')로 간략하게 적어도 작동 가능

- 파일을 open() 함수로 열어서 사용했을 때는 f.close()로 마지막에 파일을 닫아줘야 함.

```
# 아래 코드를 실행하면 py 파일이 존재하는 디렉토리 위치에 "새파일.txt" 생성됨.
f = open("새파일.txt", 'w')
f.close() # 열려있는 파일 객체를 닫아주는 역할
```

### with open() as 변수명:

- 파일을 다룰 때, with 문을 통해 작성하면 f.close() 없이도 자동으로 닫아줌

```
# 파일 여는 방법1: open()
f = open(file = 'data.txt', mode='r', encoding='utf8')
f.close() # 파일을 닫아줌


# 파일 여는 방법 2: with문은 아래 실행 부분이 완료되면 알아서 닫히기 때문에 닫을 필요 없음
with open(file='data.txt', mode='r', encoding='utf8') as f:
    pass
```

## 파일 쓰기

- f의 write 함수를 사용한 것 말고는 기존 콘솔에 쓰던 for문과 큰 차이 없음

- 이미 생성 후 작성된 파일을 다시 'w'로 불러와 내용을 추가하면 기존 내용에 덮어씌어 짐

- 파일을 쓸 때 뉴라인 캐릭터(\n)을 넣어주지 않을 경우 한줄에 연이어 작성됨

```
# 단계2: 파일 쓰기
# 쓰기 모드('w')로 작성하고자하는 경로의 파일 열기(파일이 없다면 먼저 생성)
# 작성법은 for문과 거의 흡사. print() 함수 대신에 f.write() 함수 사용
# 항상 마지막은 파일 닫기
f = open("/Users/geunwon/Documnents/C/새파일.txt", 'w')
for i in ranga(1, 11):
    data = "%번째 줄입니다. \n" % i
    f.write(data)
f.close()

# 위와 주고 차이 비교: 콘솔창에 출력할 때와 큰 차이 없음
for i in rnage(1, 11):
    data = "%번째 줄입니다. \n" % i
    print(data)

# 1줄씩 파일에 쓰기 방법1
with open(data.txt, 'w') as f:
    f.write('line 1\n')
    f.write('line 2\n')

# 1줄씩 파일에 쓰기 방법 2
with open(data.txt, 'w') as f:
    f.write('line 1', file=f) # file 옵션은 디폴트로 none을 가지고 있음
    f.write('line 2', file=f)

```

## 파일 읽기

### 커서 단위로 읽기

- read() 함수는 파라미터로 정수를 입력 받는데, 입력 받은 숫자만큼의 글자를 받아서 반환해 줌.

- 이는 파일을 open() 했을 때, 파일 제일 첫 부분의 커서가 위치하는데 read() 를 실행하면 커서가 숫자만큼 데이터를 읽어오고 다시 커서를 그 자리에 위치시킴

- 이에 read() 메서드를 게속 실행시키면 커서가 계속 움직이기 때문에 데이터가 없어 아무것도 반환하지 않음.

- 이럴 때, 다시 커서를 맨 처음에 위치시키고 싶으면 seek() 메서드를 이용

```
# 파일 읽는 방법 기본 예시
with open(file='data.txt', mode='r', encoding='utf8') as f:
    print(file.read()) # 전체 데이터를 읽어 출력함

print(f.closed) # 파일이 잘 닫혔는지 확인 가능(닫혀 있으면 True)

# 원하는 갯수만큼 데이터 읽기
with open(file='data.txt', mdoe='r', encoding='utf8') as f:
    print(f.read(10)) # 시작점부터 10칸의 데이터를 불러옴
    print(f.read(3)) # 그 뒤부터 3개의 데이터를 불러옴

# 파일 2번 읽기 예시 1: 커서의 위치 때문에 데이터를 1번만 읽어옴
with open(file='data.txt', mode='r', encoding='utf8') as f:
    print(f.read()) # 전체 데이터를 불러오고 파일 맨 뒤에 커서가 위치함
    print(f.read()) # 맨 뒤에 위치하기 때문에 불러올 데이터가 없어 아무것도 반환하지 않음.

# 파일 2번 읽기 예시 2: 파일 2번 읽어옴
with open(file='data.txt', mode='r', encoding='utf8') as f:
    print(f.read()) # 전체 데이터를 불러오고 파일 맨 뒤에 커서가 위치함
    f.seek(0) # 맨 처음 위치로 커서를 이동시킴
    print(f.read()) # 커서가 맨 처음에 위치하기 때문에 전체 데이터 불러옴
```

### 라인 단위로 읽기

- 라인 단위로 읽는 방법은 1개의 line씩 불러오는 방법과 모든 line을 불러오는 방법이 있음

- "f.readlind()"은 데이터를 1개의 line씩 불러오는 메서드로 처음부터 쭉 읽어오가다 "\n'을 만나면 읽기를 멈추고 읽은 데이터를 반환해 줌

- f.readlines()는 줄 단위로 리스트에 담아줌

```
# 파일 한줄 읽기: f.readline()
f = open("/Users/geunwon/Documnents/C/새파일.txt", 'r')
line = f.readline()
print(line) 맨 첫줄 출력
f.close()

# while문을 사용하여 모든 line불러오기
f = open("/Users/geunwon/Documnents/C/새파일.txt", 'r')
while True:
    line = f.readline()
    if not line:break # line이 없다면 빠져나와라
    print(line)
f.close()

# 데이터를 1줄씩 리스트에 요소로 넣어 출력하기
with open(file='data.txt', mode='r', encoding='utf8') as f:
    print(f.readlines()) # 전체 데이터를 1줄씩 리스트의 요소로 넣어 저장 후 리스트 반환

# for 문을 사용하여 모든 line을 불러오기
f = open("C:/doit/새파일.txt", 'r')
lines = f.readlines() # [] 안에 1줄씩 요소로 넣어 lines 변수에 담음
for line in lines:
    print(line) # 모든 라인을 1줄씩 불러옴
f.close()
```

## 파일 내용 추가하기

- 기존 파일 내용 마지막 부분에 내용 추가할 때는 'a' 모드로 열어 줌.

- 기존 파일 마지막 부분이 줄 바꿈이 되었는지 확인한 후 추가

```
f = open("/Users/geunwon/Documnents/C/새파일.txt", 'a')
for i in range(11, 20):
    data = "%d번째 줄 입니다. \n % i
    f.write(data)
f.close()
```

### 📌 참고 블로그

<br>

[파이썬 기초-파일 읽고 쓰기](https://velog.io/@jewon119/01.Python-%EA%B8%B0%EC%B4%88-%ED%8C%8C%EC%9D%BC-%EC%9D%BD%EA%B3%A0-%EC%93%B0%EA%B8%B0)
