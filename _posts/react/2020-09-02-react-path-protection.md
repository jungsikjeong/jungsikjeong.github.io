---
layout: post
title: React 경로 보호 설정하기
category: react
tags: [react, next]
comments: true
---

# React 경로 보호 설정하기

> 유데미에서 공부하면서 조금 새로운 코드를 봤습니다. 코드 정리겸 나중에 다시 사용할 수 있도록 정리하려고합니다. (거의 복붙예정)

## 경로보호란 무슨 말 인가?

- 프론트단에서 로그인안한 사용자가 접근시 접근을 못하게하거나, 다른 경로로 강제이동시키는 경우를 말한다.

## 코드

- component> routing> PrivateRoute.js

```javascript
import React from 'react';
import { Route, Redirect } from 'react-router-dom';
import PropTypes from 'prop-types';
import { connect } from 'react-redux';

const PrivateRoute = ({
  component: Component,
  auth: { isAuthenticated, loading },
  ...rest
}) => (
  <Route
    {...rest}
    render={(props) =>
      !isAuthenticated && !loading ? (
        <Redirect to='/login' />
      ) : (
        <Component {...props} />
      )
    }
  />
);

PrivateRoute.propTypes = {
  auth: PropTypes.object.isRequired,
};

const mapStateToProps = (state) => ({
  auth: state.auth,
});

export default connect(mapStateToProps)(PrivateRoute);
```

- App.js

```javascript
<PrivateRoute exact path='/dashboard' component={Dashboard} />

// <Route exact path='/dashboard' component={Dashboard} /> 에서
// <PrivateRoute exact path='/dashboard' component={Dashboard} /> 로 바뀐것임
```
