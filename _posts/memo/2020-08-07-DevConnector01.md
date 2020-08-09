---
layout: post
title: DevConnector 프로젝트 01 - 내겐 조금 생소한 코드 - 서버
category: memo
tags: [memo]
comments: true
---

# DevConnector 프로젝트 01 - 내겐 조금 생소한 코드 - 서버

## express에 bodyParser가 통합됬다?

- 유데미 강의에서 서버단을 설정하고있는데 조금 생소한 코드가 등장했다.<br>
  오래전 노마드코더 유튜브 클론 코딩 강의에서 express를 사용할때는 bodyParser를 명시해줬는데, 이제는 express가 통합되면서 명시해주지 않아도 되나보다.<br>

```javascript
const express = require('express');
const connectDB = require('./config/db');

const app = express();

// Connect Database
connectDB();

// Init Middleware
// bodyParser 미들웨어의 여러 옵션 중에 하나로,
// bodyParser가 express에 흡수되서 따로 명시해주지않아도된다.
app.use(express.json({ extended: false }));

app.get('/', (req, res) => res.send('API Running'));

// Define Routes
app.use('/api/users', require('./routes/api/users'));
app.use('/api/auth', require('./routes/api/auth'));
app.use('/api/profile', require('./routes/api/profile'));
app.use('/api/posts', require('./routes/api/posts'));

const PORT = process.env.PORT || 5000;

app.listen(PORT, () => console.log(`Server started on PORT ${PORT}`));
```

## express-validator?

- express-validator는 유효성을 검사한다고한다. Ex)회원가입시 중복된 닉네임 혹은 이메일 검사 등등..

- 그럼 사용은 어떤식으로 할까?<br>
  > [참고자료](https://express-validator.github.io/docs/)

```javascript
// users.js
const express = require('express');
const router = express.Router();
const { check, validationResult } = require('express-validator');

// @route   POST api/users
// @desc    Register user
// @access  Public
router.post(
  '/',
  [
    check('name', 'Name is required').not().isEmpty(),
    check('email', 'Please include a valid email').isEmail(),
    check(
      'password',
      'Please enter a password with 6 or more characters'
    ).isLength({ min: 6 }),
  ],
  (req, res) => {
    const errors = validationResult(req);
    if (!errors.isEmpty()) {
      return res.status(400).json({ errors: errors.array() });
    }
    res.send('User route');
  }
);

module.exports = router;
```

## express-validator 포인트

### 포인트 1

```
check('name', 'Name is required').not().isEmpty(),
```

- `'Name is required'` 이런식으로 중간에 에러메시지를 작성해줄수 있다.<br><br>

### 포인트 2

```javascript
(req, res) => {
  const errors = validationResult(req);
  if (!errors.isEmpty()) {
    return res.status(400).json({ errors: errors.array() });
  }
  res.send('User route');
};
```

- `const errors = validationResult(req);`로 유효성 검사값을 변수에 집어넣어 현재 상태값을 응답해줄 수 있는데, 유효한 값이 아니면 에러메시지가 다음처럼 나타난다.

<center>
 <figure>
 <img src="https://media.vlpt.us/images/wndtlr1024/post/fbde8d04-89bc-43af-ad49-1893238b4c69/image.png" alt="views">
 <figcaption>포스트맨에서 email, password 유효성 실패 메시지를 출력해주는 모습..</figcaption>
 </figure>
 </center>
 <br>

- 반대로 유효한 값을 입력하면 설정해줬던 `res.send('User route');` 메시지가 잘 나타난다.

<center>
 <figure>
 <img src="https://media.vlpt.us/images/wndtlr1024/post/7d79c372-aaf7-4f05-827b-56415273b901/image.png" alt="views">
 <figcaption>포스트맨에서 email, password성공시 메시지를 출력해주는..</figcaption>
 </figure>
 </center>
