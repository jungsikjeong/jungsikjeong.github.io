---
layout: post
title: next에서 customErrorPage 설정해보기
category: react
tags: [react, next]
comments: true
---

# next에서 customErrorPage 설정해보기

> 에러가 발생했을때 에러 페이지를 설정해봅니다.

## \_error.js 커스텀 마이징하기

- 넥스트에선 \_error.js파일이라는 에러발생시 보여주는 화면을 커스텀마이징 할 수 있다.

## pages/about.js

- const statusCode = res.status > 200 ? res.status : false; 이 부분을 중점으로 보면될것 같다.

```javascript
import React, { Component, useEffect, useState } from "react";
import Link from "next/link";
import fetch from "isomorphic-unfetch";
import Layout from "../components/Layout";
import Error from "./_error";

const About = ({ user, statusCode }) => {
  About.getInitialProps = async () => {
    const res = await fetch("https://api.github.com/users/jungsikjeong");
    const statusCode = res.status > 200 ? res.status : false;
    const data = await res.json();

    return { user: data, statusCode };
  };

  if (statusCode) {
    console.log(statusCode);
    return <Error statusCode={statusCode} />;
  }

  // const { user, statusCode } = props;
  return (
    <Layout title="About">
      <p>{user.name}</p>

      <p>A javaScript programmer</p>
      <img src={user.avatar_url} alt="Reed" height="200px" />
    </Layout>
  );
};

export default About;
```

## \_error.js

```javascript
import Layout from "../components/Layout";

export default ({ statusCode }) => (
  <Layout title="Error!!!">
    {statusCode
      ? `사용자 데이터를 로드 할 수 없습니다: Status code ${statusCode}`
      : `해당 페이지를 가져올 수 없습니다. 죄송합니다`}
  </Layout>
);
```
