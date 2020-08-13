---
layout: post
title: DevConnector 프로젝트 00 - 초기세팅
category: memo
tags: [memo]
comments: true
---

# DevConnector 프로젝트 00 - 초기세팅

> [유데미 강의](https://www.udemy.com/course/mern-stack-front-to-back/learn/lecture/10055140?start=225#overview)를 보며 정리한 내용입니다. 영어로 듣고 화면만 보며 따라치고 잘 모르겠는 개념이 나오면 구글링후 메모하는 용도로 만들었습니다.<br>
> 틀린 내용이 있다면 편하게 댓글로 알려주세요!

## 초기 세팅

```
npm i express express-validator bcryptjs request config gravatar jsonwebtoken mongoose axios
npm i -D nodemon concurrently
```

- express-validator: 유효값 검사를 한다. Ex)회원가입시 중복된 닉네임 혹은 이메일 검사

  - [자세히](https://2ssue.github.io/programming/express-validator/)<br>

- concurrently:리액트 서버와 express 서버를 동시 실행해주는 역할을 한다.

- npm i request: 브라우저에서 자바스크립트를 쓴다면 Fetch라는 내장 모듈이 있지만 Node.js에서 가장 많이 HTTP 네트워크 라이브러리는 단연 Request.js이다.

  - [자세히](https://medium.com/harrythegreat/node-js%EC%97%90%EC%84%9C-request-js-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-28744c52f68d)<br>

- gravatar: 아바타를 편하게 가져와준다.

## server.js 및 라우터

> 이 강의에서는 프론트서버만 나누고, 서버폴더를 따로 두지않습니다.(아직 까진 서버쪽 세팅중이라 프론트폴더는 생성 전 입니다.)<br>
> 기본적인 라우터를 생성 및 연결하고, config/db.js를 불러와 서버에 몽고db를 연결해줍니다.

- server.js

```javascript
const express = require('express');
const connectDB = require('./config/db');

const app = express();

// Connect Database
connectDB();

app.get('/', (req, res) => res.send('API Running'));

// Define Routes
app.use('/api/users', require('./routes/api/users'));
app.use('/api/auth', require('./routes/api/auth'));
app.use('/api/profile', require('./routes/api/profile'));
app.use('/api/posts', require('./routes/api/posts'));

const PORT = process.env.PORT || 5000;

app.listen(PORT, () => console.log(`Server started on port${PORT}`));
```

- routes/api/auth
  > 이후 routes/api/users,posts,profile파일도 다 똑같이 세팅

```javascript
const express = require('express');
const router = express.Router();

// @route   Get api/auth
// @desc    Test route
// @access  Public
router.get('/', (req, res) => res.send('User route'));

module.exports = router;
```

## config폴더 구성 및 db.js

- config/db.js

```javascript
const mongoose = require('mongoose');
const config = require('config');
const db = config.get('mongoURI');

const connectDB = async () => {
  try {
    await mongoose.connect(db, {
      useUnifiedTopology: true,
      useNewUrlParser: true,
    });

    console.log('MongoDB Connected...');
  } catch (err) {
    console.error(err.message);
    // 실패한 프로세스 종료
    process.exit(1);
  }
};

module.exports = connectDB;
```

- config/default.json

```
{
  "mongoURI": "mongodb+srv://<몽고ID>:<password>@@cluster0.pr8qg.mongodb.net/<dbname>?retryWrites=true&w=majority"
}

```

## 최종 프로젝트 구조

<img src="https://media.vlpt.us/images/wndtlr1024/post/e3636b35-6c03-4dda-90c7-eb88ae9f984f/image.png" alt="views">

`: 이 카테고리는 개인 메모를 하는곳이므로, 이후 개발진행과정은 자세한 포스팅은 하지않겠습니다.`
