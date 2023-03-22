---
layout: post
title: Ajax와 Axios, fetch
tags: [Javascript, Web]
categories:
  - WEB
date: 2023-03-22
---

# Ajax

Ajax는 Asynchronous JavaScript And XML의 약자.
JavaScript를 사용한 비동기 통신, 클라이언트와 서버간의 데이터를 주고 받는 기술.

HTML과 다른 기술들을 사용하는 새로운 접근법이라고 설명하기도 함. Ajax를 통해 서버와 비동기적으로 통신함으로 인해, 전체 웹페이지를 다시 불러오는 동기 방식과는 다르게 점진적으로 해당 부분의 사용자 인터페이스를 갱신할 수 있음.

즉, Ajax는 JavaScript에서 비동기 HTTP 통신이 가능하도록 해줌. 비동기 HTTP 통신이란 response와 request를 비동기 식으로 다룰 수 있는 것을 의미함.

Ajax의 가장 핵심적인 구성 요소는 바로 XMLHttpRequest 객체임. Ajax에서 XMLHttpRequest 객체는 웹 브라우저가 서버와 데이터를 교환할 때 사용됨. 콜백 시옥이 생길 수도 있음.

## jQuery와의 관계

보통의 상황에서 Ajax라는 말을 사용할 때를 보면 jQuery의 Ajax를 말할 때가 많음. 그렇지만 이는 조금 잘못됨.

Ajax를 jQuery를 통해 더 쉽게 사용할 수 있기에 jQuery와 Ajax를 함께 묶어서 말할 때가 많은 것임. Ajax의 기술 자체는 2005년부터 쓰여옴. 하지만 코드가 지저분해서 이에 대한 보완이 필요했고 그러던 중 JQuery에서 Ajax를 편리하게 사용할 수 있도록 정립하면서 jQuery가 급부상하게 됨. 또한 jQuery를 사용하여 Ajax를 구현할 경우 브라우저에 구현받지 않고 동일한 코드로 같은 작업을 구현할 수 있음.

## 순수 ajax와 jQuery ajax의 비교

- 순수 Ajax를 사용하는 경우

```
function reqListener (e) {
    console.log(e.currentTarget.response);
}

var oReq = new XMLHttpRequest();
var serverAddress = "https://jsonplaceholder.typicode.com/posts";

oReq.addEventListener("load", reqListener);
oReq.open("GET", serverAddress);
oReq.send();
```

- jQuery를 통해 Ajax를 사용하는 경우

```
var serverAddress = 'https://jsonplaceholder.typicode.com/posts';

// jQuery의 .get 메소드 사용
$.ajax({
    url: ,
    type: 'GET',
    success: function onData (data) {
        console.log(data);
    },
    error: function onError (error) {
        console.error(error);
    }
});
```

jQuery를 통해 Ajax를 사용할 때 코드가 훨씬 간단해지고 직관적임. 뿐만 아니라 그냥 Ajax만을 사용할 때는 브라우저 간 호환성에 염두해두고 각기 다른 코드를 작성해야 하는 경우가 있는데 jQuery를 사용할 경우 호환성에 대해서도 보장이 됨.

# Axios

기존에 WEB에서 어떤 리소스를 비동기로 요청하기 위해서는 XHR(XML HTTP Request)객체를 사용해야 했는데 XHR은 잘 디자인되어 있는 API가 아님. 요청의 상태나 변경을 구독하려면 Event를 등록해서 변경사항을 받아야 했고 요청의 성공, 실패 여부나 상태에 따라 처리하는 로직이 들어가기 좋지 않았음.

이를 보완하기 위해 HTTP 요청에 최적화 되어 있고 상태도 잘 추상화 되어 있는 API들이 생겨나기 시작함.

Axios는 node.js와 브라우저를 위한 Promise 기반의 HTTP 통신 라이브러리임.

비동기로 HTTP 통신을 가능하게 해주며 return을 promise 객체로 해주기 때문에 response 데이터를 다루기도 쉬움.

react를 사용한다면 fetch보다 Axios가 좋음.

크로스 브라우징 기반으로 브라우저 호환성이 뛰어남.

자동으로 json 데이터 형식으로 변환되고 요청 취소 및 타임아웃 설정이 가능.

fetch에 존재하지 않는 기능이 좀 더 많음.

XSRF 해킹 기법에 비교적 안전함.

라이브러리 설치가 필요함(import 필요)

- Axios의 post method 구현

```
axios({
  method: 'post',
  url: '/user/12345',
  data: {
    firstName: 'Yongseong',
    lastName: 'Kim'
  }
});
```

# fetch

fetch는 ES6부터 JacaScript의 내장 라이브러리로 들어옴. promise 기반으로 만들어져서 Axios와 마찬가지로 데이터를 다루는데 어렵지 않음. 내장 라이브러리이기 때문에 import없이 사용 가능함.
XMLHttpRequest 대체자로 나온 것이 fetchAPI임. 비동기 HTTP 요청을 더 쓰기 편하게 해 줌.

React Native같은 잦은 업데이트에도 잘 적용이 됨

기본 응답 결과는 Response 객체임. json으로 바꾸거나 text로 바꾸는 처리 과정이 필요함.
구형 브라우저에서는 지원을 안하고 네트워크 에러 발생시 계속 기다려야함.  
API 요청을 취소할 수가 없음.

```
const url ='http://localhost3000/test`
const option ={
   method:'POST',
   header:{
     'Accept':'application/json',
     'Content-Type':'application/json';charset=UTP-8'
  },
  body:JSON.stringify({
  	name:'sewon',
    	age:20
  })

  fetch(url,options)
  	.then(response => console.log(response))
}
```

### 📌 참고 블로그

<br>

[Ajax와 Axios 그리고 fetch](https://velog.io/@kysung95/%EA%B0%9C%EB%B0%9C%EC%83%81%EC%8B%9D-Ajax%EC%99%80-Axios-%EA%B7%B8%EB%A6%AC%EA%B3%A0-fetch)

[비동기 HTTP 통신 종류](https://ghost4551.tistory.com/139)
