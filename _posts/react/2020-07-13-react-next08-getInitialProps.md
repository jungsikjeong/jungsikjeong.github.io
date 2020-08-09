---
layout: post
title: getInitialProps로 api데이터 가져오기
category: react
tags: [react, next]
comments: true
---

# getInitialProps로 api데이터 가져오기

## getInitialProps란?

- next는 서버로부터 동적인 데이터를 가져오지 못한다.그래서 프론트에서 동적인데이터를 사용 할 수 있게끔 도와주는 함수이다.

- 컴포넌트디드마운트,컴포넌트윌마운트 같은 라이프사이클의 일종으로 넥스트가 임의로 추가해준 라이프 사이클이다.

- 어떤 작업보다도 `최초로 실행`된다.
  (이후에 서버사이드랜더링할때도 getInitialProps를 활용하는듯하다.)

## 사용

> isomorphic-unfetch는 데이터를 가져올 때 사용할 라이브러리입니다. 브라우저 [fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) API 구현을 간단히 할 수 있도록 만들어진 것입니다.

```
npm i isomorphic-unfetch
```

```javascript
import React, { Component, useEffect, useState } from "react";
import Link from "next/link";
import fetch from "isomorphic-unfetch";
import Layout from "../components/Layout";

const About = (props) => {
  About.getInitialProps = async () => {
    const res = await fetch("https://api.github.com/users/jungsikjeong");
    const data = await res.json();

    return { user: data };
  };

  const { user } = props;
  return (
    <Layout title="About">
      <p>{user.name}</p>
      {/* {JSON.stringify(props.user)} */}

      <p>A javaScript programmer</p>
      <img src={user.avatar_url} alt="Reed" height="200px" />
    </Layout>
  );
};

export default About;
```

## 개인적으로 사용하면서 헤맸던 부분

: About컴포넌트의 인자로 props를 안써줘서 화면에 null이 표시됬다. 화면에 뿌릴때도

```
JSON.stringify(props.user)
```

로 props.user를 사용하여 접근해야한다.<br>
본문의 코드는 `const { user } = props;` es6문법을 사용해서 바로 접근할수 있게 해줬다.

### 코드 업데이트

```javascript
import React, { Component, useEffect, useState } from "react";
import Link from "next/link";
import fetch from "isomorphic-unfetch";
import Layout from "../components/Layout";

const About = ({ user }) => {
  About.getInitialProps = async () => {
    const res = await fetch("https://api.github.com/users/jungsikjeong");
    const data = await res.json();

    return { user: data };
  };

  return (
    <Layout title="About">
      <p>{user.name}</p>
      {/* {JSON.stringify(props.user)} */}

      <p>A javaScript programmer</p>
      <img src={user.avatar_url} alt="Reed" height="200px" />
    </Layout>
  );
};

export default About;
```

- props를 ({}) es6문법을써서 바로 가져올수있게해줬다.
