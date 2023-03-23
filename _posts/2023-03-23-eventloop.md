---
layout: post
title: Event Loop
tags: [Javascript, Web]
categories:
  - WEB
date: 2023-03-23
---

# JavaScript는 싱글스레드 언어?

- JavaScript는 싱글스레드(단일스레드) 언어로 한 번에 하나의 작업만을 처리할 수 있음.

- 비동기로 동작하기 때문에 단일스레드임에도 불구하고 동시에 많은 작업을 수행함.

- 하지만 비동기로 동작하는 핵심 요소는 자바스크립트가 아닌 브라우저가 가지고 있음.(Node의 경우 libuv 라이브러리)

# 브라우저의 기본 구조

브라우저는 Web APIs, Event Table, callback Queue, Event Loop 등으로 구성되며 자바스크립트 코드가 실행될 때 브라우저와의 동작은 아래 설명.

## JS

- Heap : 메모리 할당이 발생하는 곳

- Call Stack : 실행된 코드의 환경을 저장하는 자료구조로, 함수 호출 시 이곳에 저장됨. 어떤 함수를 저장하면 스택에 쌓고 또 다른 함수를 호출하면 그 다음 스텍에 쌓이면서 가장 위에 쌓인 함수를 가장 먼저 처리함. LIFO(Last In First Out, 후입선출)

## Web APIs

Web API는 브라우저에서 제공하는 API로 DOM(document), Ajax(XMLHttpRequest), setTimeout 등이 있음.

## Event Table

특정 event(timeout, click, mouse move 등)가 발생했을 때 어떤 callback 함수가 호출되야 하는지를 알고 있는 자료구조임.

## Callback Queue

함수를 저장하는 자료구조로, Call Stack과 다르게 가장 먼저 들어온 함수를 가장 먼저 처리함. FIFO(First In First Out, 선입선출)

## Event Loop

- call stack과 callback Queue를 감시

- 이벤트 루프는 call stack이 다 비워지면 callback queue에 존재하는 함수를 하나씩 call stack으로 옮기는 역할을 함.

# 이벤트 루프 과정

```
function main(){
  console.log('First');
  setTimeout(
    function display(){
      console.log('Second');
    }
  ,0);
  console.log('Third');
}
main();

//Output
//First
//Third
//Second
```

'First'와 'Third' 2개의 console.log와 그 사이에 0ms의 대기 시간으로 콘솔에 'Second'를 보여주는 setTimeout함수가 끼워져 있음.

결과값을 보게 되면 First => Second => Third 순서가 아닌 First => Third => Second 순서로 나오게 됨.

- main 함수에 대한 호출이 먼저 call stack에 추가(push)됨. 그런 다음 브라우저는 main 함수의 첫 번째 명령문인 console.log('First')를 스택으로 추가됨.  
  console.log('First')가 실행되어 화면에 출력한 뒤, call stack에서 제거 됨.

- 다음 명령문인 setTimeout이 call stack에 추가되고 실행이 되면서 브라우저가 제공하는 timer Web API를 호출한 후에 call stack에서 제거됨.

- console.log('Third')는 브라우저에서 timer가 실행되는 동안 스택에 추가가 되며 이 경우 0ms의 시간만큼 지연이 되기 때문에 브라우저에서 콜백을 수신하는 즉시 메시지 대기열에 콜백이 추가 됨.

- main 함수에서 마지막 명령문이 실행된 후 main 함수가 call stack 튀어나와 call stack이 비어있게 됨. 브라우저가 대기열인 message queue에서 call stack으로 메시지를 추가하려면 먼저 call stack이 비워있어야 함. 바로 이것 때문에 setTimeout에서 제공된 지연시간이 0ms임에도 다른 모든 것들이 실행이 완려될 때까지 기다려야 하는 이유임.

- 이제 콜백이 call stack으로 추가되어 실행됨. console.log('Second')가 실행이 되며 이것이 자바스크립트의 이벤트 루프임.

### 📌 참고 블로그

<br>

[이벤트 루프란?](https://velog.io/@seokkitdo/%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EB%A3%A8%ED%94%84%EB%9E%80)

[JavaScript 비동기 핵심 Event Loop 정리](https://medium.com/sjk5766/javascript-%EB%B9%84%EB%8F%99%EA%B8%B0-%ED%95%B5%EC%8B%AC-event-loop-%EC%A0%95%EB%A6%AC-422eb29231a8)
