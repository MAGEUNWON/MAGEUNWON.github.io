---
layout: post
title: Query String
tags: [api, web]
categories:
  - WEB
date: 2023-05-16
---

# Query String

참가신청서 list API를 만드는 작업 중 POST 요청을 GET 요청으로 변경하는것이 좋겠다는 의견이 들어왔다!
그래서 GET으로 바꾸기 위해 쿼리스트링을 사용하게 되었음!

쿼리스트링은 기존에 써본적이 있긴 하지만 회사 들어와서는 pagination에서 사용해본것이 전부였기 때문에 좀 더 알아보았다😀

우선 왜 list API가 POST가 아니라 GET이 더 적합한지부터 찾아봤다.

## GET vs POST

✅ GET

일반적으로 GET 요청은 서버로부터 데이터를 가져오는데 사용됨. GET 요청은 URL에 매개변수를 포함하여 데이터를 전다하며, 브라우저에서 캐시될 수 있고 북마크로 저장될 수도 있음. GET 요청은 주로 데이터를 조회하는 용도로 사용됨. 즉, 데이터를 조회하는 경우에 적합함.

✅ POST

POST 요청은 서버로 데이터를 제출하는 데 사용됨. POST 요청은 데이터를 요청 본문에 포함하여 전달하며, 주로 사용자가 양식을 작성하거나 파일을 업로드하는 등의 작업에 사용됨. POST 요청은 데이터가 URL에 노출되지 않으므로 GET 요청보다 보안적으로 더 안전함. 또한 POST 요청은 서버에 상태 변경을 요청하거나 데이터를 생성하는 등의 작업에 적합함.

📌 따라서 내가 작업하고 있던 list API는 데이터를 조회하고 결과를 반환하는 용도로 사용되는 것이기 때문에 GET 요청이 적합한 것이었음!

## Query String 이란?

쿼리 문자열은 URL의 끝에 ? 기호로 시작하고, key=value 형식의 매개변수를 & 기호로 구분하여 추가할 수 있음.

쿼리스트링의 ? 뒤 Parameters 부분이 Query Parameter임.

흔히 쿼리 스트링, 쿼리 파라미터라고 부름. 둘은 같은 표현이다.

쿼리스트링은 key와 value로(key=value) 쌍을 이룬 문자 형태이며 이 형태로 매개변수를 전달하는 방식임. 여러개의 매개변수는 &로 연결한다. 쿼리스트링은 주로 GET 요청에서 사용되며, URL의 일부로 데이터를 전달하는데 적합함!

이렇게 담겨진 Query String은 웹 서버로 전달 됨. 전달된 매개변수는 서버에서 파싱하여 사용할 수 있음.

✅ 비교할 것으로 Path Variable이 있음.

### Path Variable(경로 변수)

경로 변수는 URL 자체의 경로에 데이터를 포함하는 방식. 경로의 일부로 데이터를 전달하여 동적인 URL을 생성할 수 있음.

예를 들어, /api/endpoint/value1/value2와 같은 형식으로 경로 변수를 포함한 URL을 생성할 수 있다.

경로 변수는 주로 RESTful API에서 사용되며, 특정 자원을 식별하거나 조작하기 위해 사용함!

### 각각 언제 사용?

두 방식은 데이터 전달 방식에 차이가 있음. 쿼리스트링은 매개변수를 key=value 형식으로 URL에 추가하여 전달하며, 경로 변수는 URL 자체의 경로에 데이터를 포함하여 전달함. 데이터 전달 방식이나 사용하는 시나리오에 따라 어떤 방식을 선택해야 할지 결정 할 수 있음.

📌 Query Parameter : 정렬이나 필터링을 한다면 Query Parameter를 사용

```
/users?=id=123 // id가 123인 사용자 정보 가져오기
```

📌 Path Variable : resource를 식별, 특정 인덱스에 대한 조회 하고 싶으면 Path Variable을 사용

```
GET/users/123 // id가 123인 사용자 정보 가져오기
```

<br>

### 📌 참고 블로그

[[번역] Path Variable과 Query Parameter는 언제 사용해야 할까?](https://ryan-han.com/post/translated/pathvariable_queryparam/)
