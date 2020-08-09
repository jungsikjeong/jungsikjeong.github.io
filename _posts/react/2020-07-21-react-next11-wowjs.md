---
layout: post
title: wowjs를 활용하여 리액트에서 애니메이션 구현하기
category: react
tags: [react, next]
comments: true
---

#  wowjs를 활용하여 리액트에서 애니메이션 구현하기
> wowjs깃허브주소:[wowjs](https://github.com/matthieua/WOW)<br>
> 구현 할 수 있는 css목록들:[animate](https://animate.style/)


## wowJs사용전 준비단계
> 최신버전인 4.1.0 링크코드를 복붙했으나 css가 동작하지않았습니다. 혹시 이 글을 보고 최신버전으로 사용해보신분은 댓글로 알려주시면 감사하겠습니다!<br>


- npm i wowjs

- public/index.html파일의 head태그 안에 다음 코드를 복사 붙여넣기
  
```javascript
  <link
      rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.5.2/animate.min.css"
    />
```

## wowJs사용
> className에 `wow`를 넣고,적용할 애니메이션 이름을 넣으면 됩니다. 이후 옵션을넣으면됩니다. 자세한건 [wowjs](https://github.com/matthieua/WOW) 참고해주세요.

- index.css

```css
body {
  margin: 0;
  padding: 0;
  font-family: sans-serif;
}

.center {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 80vh;
  width: 100%;
}

.center-photo {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  height: 80vh;
  width: 100%;
}

h1 {
  font-size: 4em;
}

.photo {
  max-height: 200px;
}

```

- App.js

```javascript
import React, { useEffect } from 'react';
import WOW from 'wowjs';

const App = () => {
  useEffect(() => {
    new WOW.WOW().init();
  }, []);

  return (
    <div>
      <div className='center'>
        <h1 className='wow flipInY' data-wow-iteration='1'>
          Hello Word!
        </h1>
        <p>a how to about WOW.js</p>
      </div>

      {/* offset은 요소까지의 거리 기본값은 0. 이라고 설명되어있는데,
      유저가 보는 화면 스크롤?이 어느정도왔을때 애니메이션이 발동되는지를 말하는듯 하다 */}
      <div className='center-photo'>
        <img
          className='photo wow fadeInDown'
          data-wow-iteration='1'
          data-wow-offset='80'
          data-wow-delay='.5s'
          src='/alaska1.jpg'
          alt='views'
        />
        <img
          className='photo WOW fadeInDown'
          data-wow-iteration='1'
          data-wow-offset='80'
          data-wow-delay='.75s'
          src='/alaska2.jpg'
          alt='views'
        />
        <img
          className='photo WOW fadeInDown'
          data-wow-iteration='1'
          data-wow-offset='80'
          data-wow-delay='1s'
          src='/alaska3.jpg'
          alt='views'
        />
      </div>
    </div>
  );
};

export default App;
```

### 결과물

<img src="https://media.vlpt.us/images/wndtlr1024/post/6dc628ff-7b04-4180-811e-bb9f7581b10d/wow%EC%98%88%EC%A0%9C.gif" alt="views" />