---
title: "Node JS - Rest API 만들기"
categories:
  - settings/node
tags:
  - Server
  - Node JS
toc: true
toc_label: "Node JS - Rest API 만들기"
---

## 어떤 환경으로 실행을 했는가?

개발을 위한 환경으로 실행을 한다면, **"develop"** 이고, 실제 서비스를 위한 배포 환경으로 실행을 한다면, **"production"** 값이 들어갑니다. 따라서, 다음과 같이 이 프로젝트가 어떤 환경으로 실행되었는지를 알아볼 수 있도록 상수로 저장하여 맨 위에 선언해 둡니다.

```js
const isProduction = process.env.NODE_ENV === "production";
```

## Express JS 미들웨어 등록하기

### Express 모듈 불러오기

Express JS를 사용하기 위해서는 다음과 같이 express() 함수를 호출하여 미들웨어 및 라우팅을 등록할 수 있는 객체를 불러옵니다.

```js
const app = express();
```

### CORS 설정

CORS란 도메인 또는 포트가 다른 서버의 자원을 요청하는 것을 말합니다. 브라우저에서는 보안상 서로 다른 도메인이나 포트가 다른 서버의 자원을 요청할 수 없도록 막아두고 있습니다. 하지만, 요즘은 마이크로 서비스로 설계하는 프로젝트가 많아지고 있기 때문에 이러한 설정을 풀어줄 필요가 있습니다.
<br>
<br>
그러기 위해서는 응답 시에 CORS에 대한 헤더를 서버에서 반환해 주어야 합니다. 이런 작업을 도와주는 미들웨어가 cors 입니다.
<br>
<br>
cors 모듈을 설치한 다음, 아래와 같이 작성하면 미들웨어를 등록할 수 있습니다.

```js
import cors from "cors";

// CORS - widthCredentials
app.use(
  cors({
    origin: true,
    credentials: true
  })
);
```

### 쿠키 설정

쿠키의 값을 쉽게 추출할 수 있도록 도와주고, 쿠키를 생성하는 함수도 제공해 줍니다. 따라서, CSRF 토큰을 발급하여 쿠키에 저장하는 경우에 손쉽게 토큰을 쿠키에 저장하고 그 값을 불러와서 검증할 수 있습니다.

```shell
COOKIE_SECRET=hello_cookie
```

```js
import cookieParser from "cookie-parser";

app.use(cookieParser(process.env.COOKIE_SECRET));
```

### CSRF 설정

CSRF 공격에 대비해서 GET 요청에 한해서 XSRF-TOKEN 토큰을 발급해줍니다. (1 ~ 3 시간)
<br>
이어서 csrfProtection 미들웨어를 등록하여 토큰의 검증을 자동으로 해줍니다.
<br>
csrfProtection 은 GET 요청을 제외한 POST/PUT/DELETE 요청에 사용되는 미들웨어입니다.

```js
import csrf from "csurf";

const csrfProtection = csrf({ cookie: true });

app.get("/GET요청", csrfProtection, function (req, res) {
  res.cookie("XSRF-TOKEN", req.csrfToken(), {
    expires: new Date(Date.now() + 3 * 3600000) // 3시간 동안 유효
  });

  // ...
});
```

### JWT 설정

#### JWT 토큰 발급

```js
import csrf from "csurf";
import jwt from "jsonwebtoken";

const csrfProtection = csrf({ cookie: true });

function generateAccessToken(username) {
  return jwt.sign(username, process.env.ACCESS_TOKEN_SECRET, {
    expiresIn: "1800s" // 30분마다 갱신해야함
  });
}

app.post("/로그인", csrfProtection, function (req, res) {
  /* 로그인 요청 처리 ... */

  // 로그인 요청 성공하면 토큰 발급!
  res.cookie(
    "AccessToken",
    generateAccessToken({ username: req.body.username }),
    {
      httpOnly: true,
      expires: 0 // 브라우저를 닫을시 사라짐
    }
  );

  // ...
});
```

#### JWT 토큰 검증

```js
import csrf from "csurf";
import jwt from "jsonwebtoken";

const csrfProtection = csrf({ cookie: true });

function verifyToken(req, res) {
  // 쿠키에서 토큰 가져오기
  var token = req.cookies["AccessToken"];

  // 토큰 검증하기
  jwt.verify(token, process.env.ACCESS_TOKEN_SECRET, (err, user) => {
    if (err) {
      return res.sendStatus(403);
    }

    req.user = user;
    next();
  });
}

app.get("/내정보", verifyToken, function (req, res) {
  res.json({});
});
```

### 로그 설정

로그를 출력하기 위해 설정파일에 파라미터를 등록하고, 다음과 같이 출력 형태 및 파일을 설정할 수 있습니다.

```shell
LOG_FILE=log.txt
LOG_FORMAT=common
LOG_SIZE=10M
LOG_INTERVAL=1d
```

```js
import rfs from "rotating-file-stream";

const rfsStream = rfs.createStream(process.env.LOG_FILE || "log.txt", {
  size: process.env.LOG_SIZE || "10M",
  interval: process.env.LOG_INTERVAL || "1d",
  compress: "gzip" // compress rotated files
});

if (isProduction) {
  // 로그파일로 남기고 싶은 경우
  app.use(morgan(process.env.LOG_FORMAT || "dev"), {
    stream: process.env.LOG_FILE ? rfsStream : process.stdout
  });
} else {
  // 콘솔에만 찍고 싶은 경우
  app.use(morgan(process.env.LOG_FORMAT || "dev"));
}
```

**참조**
https://dev.to/paras594/node-js-morgan-guide-431o
