---
layout: post
title: Next _document.js커스텀마이징
category: react
tags: [react, next]
comments: true
---

# Next \_document.js커스텀마이징

## \_document.js

> 개인적으로 index.css기능이라고 생각합니다.

- next에서 보통 레이아웃은 \_app.js에서하거나, AppLayout.js를 구현후 \_app.js에서 import AppLayout해서 레이아웃을 구성한다.하지만 html이나 body 속성을 추가해야한다면 \_documents.js가 필요하다.

- `pages/_document.js` 형태로 존재해야 한다.

- 이외에도 styled-Components를 사용하려면 \_documents.js파일을 커스텀마이징 해야한다.

## \_documents.js만져보기

- 폰트 설정과 글로벌 css 설정 및 중복되는link href 적용하기

```javascript
import Document, { Head, Main, NextScript } from "next/document";

export default class MyDocument extends Document {
  render() {
    return (
      <html lang="ko-KR">
        <Head>
          <meta
            name="description"
            content="A site for my programing portfolio"
          />
          <meta charSet="utf-8" />
          <meta name="robots" content="noindex,nofollow" />
          <meta name="viewport" content="width=device-width" />
          <link
            rel="stylesheet"
            href="https://cdnjs.cloudflare.com/ajax/libs/nprogress/0.2.0/nprogress.min.css"
          />
          <link
            href="https://fonts.googleapis.com/css?family=Roboto"
            rel="stylesheet"
          />
        </Head>
        <body>
          <Main />
          <NextScript />
        </body>
        <style global jsx>{`
          body {
            font-family: "Roboto", sans-serif;
          }
        `}</style>
      </html>
    );
  }
}
```
