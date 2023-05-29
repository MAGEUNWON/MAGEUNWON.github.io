---
layout: post
title: 리눅스 텍스트 에디터
tags: [Linux]
categories:
  - Linux
date: 2023-05-29
---

# 리눅스 텍스트 에디터의 종류와 사용법

<br>

리눅스에서 텍스트 파일을 만들어 사용할 일이 있었는데 vi, vim, nano 등 종류가 다양해서 어떤 차이 점이 있는지 궁금했음!

내가 써 본 텍스트 에디터를 간단하게 살펴 보겠음!

## vi & Vim

<br>

vi는 visul editor의 약자이고 Vim은 Vi Improved(향상된 vi)의 약자임. Vim이 vi보다 더 편함. 그렇기 때문에 대부분의 리눅스에서는 vi를 호출해도 Vim이 실행되도록 내부적으로 alias를 설정해 둠.
리눅스에서는 기본적으로 Vim을 지원하지만, 유닉스(Unix)에선 vi를 기본으로 지원한다고 함.

vi와 Vim의 가장 큰 차이점을 Vim은 에디터에서 화살표 방향으로 커서의 이동이 되지만 vi는 이 방법으로 커서 이동이 안됨. 순수하게 vi만 설치되어 있다면 화살표 방향키가 아닌 h, j, k, l로 커서를 이동해야 함.

### vi(Vim) 자주 쓰이는 단축키

vi의 단축키는 대/소문자를 구분하므로 주의.
vim 에서는 입력모드와 명령모드 두 가지로 나눠짐

- 명령모드

  - i : 입력모드로 전환
  - :q : 종료
  - :q! : 저장하지 않고 강제로 종료
  - :wq : 저장하고 종료

- 입력 모드
  - l : 해당 줄의 맨 앞에 입력
  - a : 커서 뒤에 입력
  - A : 해당 줄의 맨 뒤에 입력
  - o : 아랫줄에 입력
  - O : 윗줄에 입력
  - r : 커서가 있는 글자를 바꾸면서 입력
  - x : 커서가 있는 문자 삭제
  - dd : 한 줄 삭제
  - yw : 커서가 있는 단어 복사
  - yy : 한 줄 복사
  - P : 커서 뒤에 붙여넣기
  - p : 커서 앞에 붙여넣기

## nano

nano는 가장 기본적인 편집기로 최소한의 기능만 가지고 있음.

## nano 실행하기

<br>

nano 에디터가 설치 되어 있는 경우 nano 파일명 입력하면 실행 됨. 예를 들어 nano test.text라고 치면 빈 text 파일이 만들어 지고 nano test.html, nano test.sh 등으로 만들 수 있음.

빈 파일이 열리면 내용을 입력하고 하단에 있는 nano 명령어를 통해 저장 및 나가기 등을 하면 됨.  
하단 명령어에 ^ 표시는 ctrl이라고 생각하면 됨!

<br>

### 📌 참고 블로그

<br>

[[Linux] vi, Vim의 차이 및 자주 쓰이는 단축키](https://unit-15.tistory.com/112)

[[Linux] 리눅스 텍스트 에디터와 vi와 vim, nano, gedit 차이 설명](https://blog.naver.com/PostView.naver?blogId=ycpiglet&logNo=222367301056)
