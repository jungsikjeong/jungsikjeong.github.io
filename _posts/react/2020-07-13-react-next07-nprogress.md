---
layout: post
title: next에서 nprogress사용해보기
category: react
tags: [react, next]
comments: true
---

# next에서 nprogress사용해보기

> 유데미 강의 next.js를 보고 생소한 기능을 메모했습니다. 틀린 내용은 댓글로 편하게 알려주세요!

## nprogress란?

- 프론트엔드 개발할 때 언제나 필요한 기능 중 하나가 서버의 응답을 기다리는 동안에 보여줄 로딩 표시이다. 이 로딩 표시를 간단하게 구현해준다.

## nprogress사용

- [cdnjs](https://cdnjs.com/libraries/nprogress)로 가서 nprogress.css코드를 긁어온다.

- 아래 코드 참고

### 핵심 코드 기입

> <Head> 태그 안에있는 link는 _document.js파일안에 넣어서 보관하기도한다. <br>

```javascript
<Head>
  <title>NextPortfolio</title>
  <link
    rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/nprogress/0.2.0/nprogress.min.css"
  />
</Head>;

// 라우터이동할때 로딩 설정
Router.onRouteChangeStart = (url) => {
  console.log(url);
  NProgress.start();
};
// 라우터이동이 완료했을때 설정
Router.onRouteChangeComplete = () => {
  NProgress.done();
};
// 라우터에러발생했을때 로딩 설정
Router.onRouteChangeError = () => {
  NProgress.done();
};
```

### 전체 코드

```javascript
import React from "react";
import Link from "next/link";
import Head from "next/head";
import Router from "next/router";
import NProgress from "nprogress";

// 라우터이동할때 로딩 설정
Router.onRouteChangeStart = (url) => {
  console.log(url);
  NProgress.start();
};
// 라우터이동이 완료했을때 설정
Router.onRouteChangeComplete = () => {
  NProgress.done();
};
// 라우터에러발생했을때 로딩 설정
Router.onRouteChangeError = () => {
  NProgress.done();
};
const Layout = ({ children, title }) => {
  return (
    <div className="root">
      <Head>
        <title>NextPortfolio</title>
        <link
          rel="stylesheet"
          href="https://cdnjs.cloudflare.com/ajax/libs/nprogress/0.2.0/nprogress.min.css"
        />
      </Head>
      <header>
        <Link href="/">
          <a>Home</a>
        </Link>
        <Link href="/about">
          <a>About</a>
        </Link>
        <Link href="/hireme">
          <a>Hire Me</a>
        </Link>
      </header>

      <h1>{title}</h1>
      {children}

      <footer>&copy; {new Date().getFullYear()}</footer>
    </div>
  );
};

export default Layout;
```

## 작동 화면

<center>
 <figure>
 <img src="https://media.vlpt.us/images/wndtlr1024/post/85a7b1cf-6596-4d76-b7e3-37f0f05f023f/nprogress%EC%9E%91%EB%8F%99%EB%AA%A8%EC%8A%B5.gif" alt="views">
 <figcaption>헤더부분 맨 오른쪽에 라우터 경로가 바뀔때마다 파란색 동그라미로 로딩표시가 뜬다.콘솔창에는 바뀐 url경로가 출력된다.</figcaption>
 </figure>
 </center>
