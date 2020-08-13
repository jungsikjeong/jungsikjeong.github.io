---
layout: post
title: DevConnector 프로젝트 02 - 내겐 조금 생소한 코드 - 클라이언트
category: memo
tags: [memo]
comments: true
---

# DevConnector 프로젝트 02 - 내겐 조금 생소한 코드 - 클라이언트

## setFormData({ ...formData, [e.target.name]: e.target.value });

```javascript
const [formData, setFormData] = useState({
  name: '',
  email: '',
  password: '',
  password2: '',
});

const { name, email, password, password2 } = formData;

const onChange = (e) =>
  setFormData({ ...formData, [e.target.name]: e.target.value });

<input
  type='text'
  placeholder='Name'
  name='name'
  value={name}
  onChange={(e) => onChange(e)}
  required
/>;
```

- 위의 코드에서 눈여겨 봐야할 것은 `[e.target.name]: e.target.value` 이다. <br>
  es6 비구조화 할당문법을 사용하여 코드를 간소화시켰다.

## 클라이언트에서 axios를 활용해 서버에 데이터 전송 및 데이터 받아오기

```javascript
const onSubmit = async (e) => {
  e.preventDefault();
  if (password !== password2) {
    console.log('패스워드가 일치하지 않습니다.');
  } else {
    const newUser = {
      name,
      email,
      password,
    };
    try {
      const config = {
        headers: {
          'Content-Type': 'Application/json',
        },
      };

      const body = JSON.stringify(newUser);

      const res = await axios.post('/api/users', body, config);
      console.log(res.data);
    } catch (err) {
      console.error(err.response.data);
    }
  }
};
```

- `onSubmit`부분을 주목하자. <br>
  axios를 이용해서 클라이언트에서 데이터를 전송 및 받아오는 코드에는 .then .catch 기타 등등 다양한 코드가있지만, 여기서는 `async await 를 활용해 try catch문으로 데이터 응답 및 에러를 처리`해주었다.<br>
  에러메시지를 받아오는게 좀 생소했는데, 직접 console.log(err)를 찍어본 결과, err는 객체에는 헤더 및 기타 등등의 여러 데이터가 담겨있는데 그중에서 서버에서 에러메시지를 전달해주는 response객체안의 data가있었다.<br><br>

  받아올 때는 마찬가지로 res.data로 받아온다.

> 이후 리덕스로 대체
