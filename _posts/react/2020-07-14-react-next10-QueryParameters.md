---
layout: post
title: next에서 동적으로 쿼리파라미터 변수받기
category: react
tags: [react, next]
comments: true
---

# next에서 동적으로 쿼리파라미터 변수받기

## pages/blog.js

```javascript
import Layout from "../components/Layout";
import React from "react";
import Link from "next/link";

const PostLink = ({ title }) => {
  return (
    <li>
      <Link href={`/post?title=${title}`}>
        <a>{title}</a>
      </Link>
    </li>
  );
};

const blog = () => {
  return (
    <Layout title="My Blog">
      <ul>
        <PostLink title="react" />
        <PostLink title="angular" />
        <PostLink title="vue" />
      </ul>
    </Layout>
  );
};

export default blog;
```

## pages/post.js

- withRouter를 이용하여 파라미터로 ({router})을 받는다.

```javascript
import React from "react";
import Layout from "../components/Layout";
import { withRouter } from "next/router";

const Post = ({ router }) => {
  return (
    <Layout title={router.query.title}>
      <p>
        Lorem Ipsum is simply dummy text of the printing and typesetting
        industry. Lorem Ipsum has been the industry's standard dummy text ever
        since the 1500s, when an unknown printer took a galley of type and
        scrambled it to make a type specimen book.
      </p>
    </Layout>
  );
};

export default withRouter(Post);
```

## 보다 깨끗한 url만들기

> 위의 코드처럼 하면 url에 http://localhost:3000/post?title=react 이런식으로 지저분하게 나옵니다. 조금 더 깨끗한 url로 만들어봅시다.

- Link 태그에 as를 활용한다.

```javascript
import Layout from "../components/Layout";
import React from "react";
import Link from "next/link";

const PostLink = ({ slug, title }) => {
  return (
    <li>
      <Link as={`/${slug}`} href={`/post?title=${title}`}>
        <a>{title}</a>
      </Link>
    </li>
  );
};

const blog = () => {
  return (
    <Layout title="My Blog">
      <ul>
        <PostLink slug="react-post" title="React Post" />
        <PostLink slug="angular-post" title="Angular Post" />
        <PostLink slug="vue-post" title="Vue Post" />
      </ul>
    </Layout>
  );
};

export default blog;
```

### 결과

- http://localhost:3000/react-post
- http://localhost:3000/angular-post
- http://localhost:3000/vue-post
