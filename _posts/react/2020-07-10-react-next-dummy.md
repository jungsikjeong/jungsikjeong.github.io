---
layout: post
title: react,next dummy데이터 사용해보기
category: react
tags: [react, next]
comments: true
---

# react,next dummy데이터 사용해보기

> 현업에서 백엔드 개발자와 작업을 할 때, 백엔드 서버가 아직 완성되지않았을때 프론트에서 dummy 데이터를 사용하여 임시로 작업하는 방법입니다.

## 사용예시

```
const dummy = {
  nickname: "정중식",
  Post: [],
  Following: [],
  Followers: [],
};

<Row>
  <Col xs={24} md={6}>
    {/* 유저정보 */}
    <Card
      actions={[
        <div key="twit">
          짹짹
          <br />
          {dummy.Post.length}
        </div>,
        <div key="following">
          팔로잉
          <br />
          {dummy.Post.Following.length}
        </div>,
        <div key="follower">
          팔로워
          <br />
          {dummy.Post.Follower.length}
        </div>,
      ]}
    >
      <Card.Meta
        avatar={<Avatar>{dummy.nickname[0]}</Avatar>}
        title={dummy.nickname}
      />
    </Card>
  </Col>
  <Col xs={24} md={12}>
    {children}
  </Col>
  <Col xs={24} md={6}>
    세번째
  </Col>
</Row>;
```

## 심화

> isLoggedIn을 이용해서 로그인했을때의 화면과 로그인 안했을때의 화면을 분류해줄 수 있습니다.

```js
import React from "react";
import Link from "next/link";
import PropTypes from "prop-types";
import { Menu, Input, Button, Row, Col, Card, Avatar, Form } from "antd";

const dummy = {
  nickname: "정중식",
  Post: [],
  Following: [],
  Followers: [],
  isLoggedIn: false,
};

const AppLayout = ({ children }) => {
  return (
    <div>
      <Menu mode="horizontal">
        <Menu.Item key="home">
          <Link href="/">
            <a>노드버드</a>
          </Link>
        </Menu.Item>
        <Menu.Item key="profile">
          <Link href="/profile">
            <a>프로필</a>
          </Link>
        </Menu.Item>
        <Menu.Item key="email">
          <Input.Search enterButton style={{ verticalAlign: "middle" }} />
        </Menu.Item>
      </Menu>

      <Row>
        <Col xs={24} md={6}>
          {dummy.isLoggedIn ? (
            <Card
              actions={[
                <div key="twit">
                  짹짹
                  <br />
                  {dummy.Post.length}
                </div>,
                <div key="following">
                  팔로잉
                  <br />
                  {dummy.Following.length}
                </div>,
                <div key="follower">
                  팔로워
                  <br />
                  {dummy.Followers.length}
                </div>,
              ]}
            >
              <Card.Meta
                avatar={<Avatar>{dummy.nickname[0]}</Avatar>}
                title={dummy.nickname}
              />
            </Card>
          ) : (
            <Form>
              <div>
                <label htmlFor="user-id">아이디</label>
                <br />
                <Input
                  name="user-id"
                  // value={userId}
                  // onChange={onChangeId}
                  required
                />
              </div>
              <div>
                <label htmlFor="user-password">비밀번호</label>
                <br />
                <Input
                  name="user-password"
                  type="password"
                  // value={password}
                  // onChange={onChangePassword}
                  required
                />
              </div>
              <div>
                <Button type="primary" htmlType="submit" loading={false}>
                  로그인
                </Button>
                <Link href="/signup">
                  <a>
                    <Button>회원가입</Button>
                  </a>
                </Link>
              </div>
            </Form>
          )}
        </Col>
        <Col xs={24} md={12}>
          {children}
        </Col>
        <Col xs={24} md={6}>
          세번째
        </Col>
      </Row>
    </div>
  );
};

AppLayout.propTypes = {
  children: PropTypes.node,
};

export default AppLayout;
```
