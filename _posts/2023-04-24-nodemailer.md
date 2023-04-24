---
layout: post
title: Nodemailer
tags: [node.js, javascript]
categories:
  - Node.js
date: 2023-04-24
---

# Nodemailer

이메일을 보낼 수 있는 Node.js 애플리케이션용 모듈, EmailEngine에 등록된 이메일 계정을 사용하여 이메일을 수신하고 보낼 수 있음. 기본적으로 SMTP 외에도 다양한 전송 방식을 지원하고 있으며, Unicode 인코딩을 지원하여 이모지를 사용하는 것도 가능함

## 주요 개념

- SMTP(Simple Mail Transfer Protocal)
  - 네트워크를 통해 이메일을 전송하는 기술 표준
  - Nodemailer에서 메시지 전달을 위한 주요 전송 수단
  - 메일 전송 프로토콜
  - 컴퓨터와 서버는 SMTP를 이용하여 기반 하드웨어나 소프트웨어와 관계없이 데이터를 교환

## Nodemailer 만들기

### Gmail을 이용한 메일 전송 방법

✅ 메일 전송용 Gmail 설정하기

Gmail 사용시 앱 비밀번호를 생성해서 사용해야 함. 앱 비밀번호를 사용하지 않으면 Gmail 보안 관련 에러 메시지가 뜸.  
앱 비밀번호는 보안 수준이 낮은 앱 또는 기기에 Google 계정에 대한 엑세스 권한을 부여하는 비밀번호 임.

✅ 앱 비밀번호 생성하기

앱 비밀번호를 생성하려면 우선 google 계정이 2단계 인증을 사용 중이어야 함. 2단계 인증을 사용하지 않는 다면 이것부터 할 것.

2단계 인증이 완료 됐다면

- 계정 설정 들어가기
- 보안으로 가서 Google에 로그인 이라는 항목 중 앱 비밀번호 선택
- 한번 더 비밀번호 입력 후 들어간 후 앱 비밀번호를 생성할 앱 및 기기를 선택해서 진행하면 됨. (닌 그냥 기타 선택후 이름은 nodemailer로 했음.)
- 생성하면 기기용 앱 비밀번호가 나옴. 이걸 .env 파일에 넣어 주면됨. 다시 비밀번호 볼 수 없으니 잘 저장해 둘 것.

<br>

### .env 파일 만들기

.env 파일에 이메일, 비밀번호 입력해 둠. (gitignore)

```
// .env

NODEMAILER_USER= '이메일주소'
NODEMAILER_PASS= '이메일 비밀번호'
```

- config폴더에 json 형태로 만들어도 됨.(얘도 gitignore)

```
{
	"user" : '이메일주소',
	"pass" : '이메일 비밀번호'
}
```

<br>

### mail.js

mail 모듈 만들어 주기

✅ 주어진 ID 값을 이용해 JSON Web Token(JWT)을 생성

```
resetPasswordToken: async (id) => { // access token에 들어갈 payload
    const payload = {
      id: id,
    };
    return jwt.sign(payload, secret, {
      algorithm: 'HS256', //암호화 알고리즘
      expiresIn: '10m', // 유효기간
    });
  },
```

JWT는 웹 애플리케이션에서 인증이나 권한 부여를 위해 사용되는 토큰으로, 정보를 안전하게 전달할 수 있도록 암호화된 문자열임.

함수 내에서는 주어진 id 값을 이용하여 payload라는 객체를 생성하고, 이 payload를 secret으로 암호화하여 JWT를 발급. 암호화 알고리즘으로는 HS256을 사용하고, 토큰의 유효기간은 10분으로 설정.

이 함수를 호출하면 해당 id 값을 가진 사용자에게 유효한 JWT가 생성되어 반환됨.

✅ nodemailer 라이브러리를 사용하여 이메일을 보내기

```
sendEmailPassword: async (email, number) => {
    const transporter = nodemailer.createTransport({
      sevice: 'gmail',
      host: "smtp.gmail.com",
      port: 587,
      secure: false,
      auth: {
        user: process.env.NODEMAILER_USER,
        pass: process.env.NODEMAILER_PASS,
      },
    });

  }
```

함수 내에서는 nodemailer.createTransport 메소드를 사용하여 Gmail 서비스를 사용하도록 설정. 이 메일 전송에 사용될 호스트와 포트 번호를 지정함. 그리고 보안 연결(SSL/TLS)을 사용하지 않도록 설정하고, 이메일 인증 정보를 설정하기 위해 process.env.NODEMAILER_USER와 process.env.NODEMAILER_PASS 환경변수를 사용함.

이 함수를 호출하면 설정된 인증 정보를 사용하여 이메일을 전송할 수 있는 nodemailer의 transporter 객체가 생성됨. 이후 이 trnasporter 객체를 사용하여 실제로 이메일을 전송하는 작업을 수행할 수 있음.

✅ 메일 전송

```
const info = await transporter.sendMail({
            from: process.env.NODEMAILER_USER, // sender address
            to: `${email}`, // list of receivers
            subject: " 인증번호를 위한 메일입니다.", // Subject line
            // html: "<p>" + url + "</p>",
            text: ` 인증번호는 ${number} 입니다 `
        });

        return
```

위의 transporter 객체를 사용하여 이메일을 전송하는 작업을 수행하는 비동기 함수의 나머지 부분.

함수 내에서 transporter.sendMail 메소드를 호출하여 이메일을 전송. 이메일의 보내는 사람, 받는 사람, 제목, 본문 내용 등을 설정하고, sendMail 메소드의 결과로 전송된 이메일 정보를 반환함.

이메일 전송 작업이 완료되면, 해당 작업의 결과를 반환하는 return 구문을 사용하여 함수를 종료함.

이 함수를 호출한 쪽에서는 반환된 이메일 정보를 이용하여 전송 작업의 성공 여부를 판단할 수 있음.

<br>

### 📌 참고 블로그

<br>

[nodemailer로 Gmail 보내기](https://www.cckn.dev/dev/2000-9-nodemailer/)

[[Back-end] Node.js에서 메일 전송하기 (feat. Nodemailer & Gmail)](https://velog.io/@josworks27/Back-end-Node.js%EC%97%90%EC%84%9C-%EB%A9%94%EC%9D%BC-%EC%A0%84%EC%86%A1%ED%95%98%EA%B8%B0-feat.-Nodemailer-Gmail)
