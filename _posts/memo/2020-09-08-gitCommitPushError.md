---
layout: post
title: gitCommit에러?
category: memo
tags: [memo]
comments: true
---

# gitCommit에러?

## git push 에러(?)

git init후 git push했을때 사진과 같은 현상이 발생했다.

<img src="https://cafeptthumb-phinf.pstatic.net/MjAyMDA5MDhfMjE3/MDAxNTk5NTcxMjIyNjE3.w_GmAYtpCkcJ7yJWzcHqFmVuuIMW00QltY08xppzRMcg.YpVOlMUEJ5O-3C73Xu0spL-M_Qd4hHnbi7hv450Hg_Ig.PNG/image.png?type=w1600" />

아이콘 모양이 좀 다르고, 클릭이 안된다. <br /><br />

문제가 생겼으면 당연히 원인이 있겠지만 생략하고... <br /><br />

해결방안은 의외로 심플했다.<br/>

1. Git init
2. git remote add origin “https://github.com/wjdwndtlr/travel”
3. git add .

까지 한 후에 원래는 git commit -m "커밋메시지" 후 git push origin master를 해줘야하지만,
이 과정을하면 맨 위 와같은 에러(?)가 나오므로, 3번까지만 한 후 vsCode에서 푸쉬하는 방향으로했다. (터미널 사용X)

## 새롭게 알게된 사실!!

- npx create-react-app . 하면 git init이 자동으로 된다.
- 그래서 git 디렉토리가 만들어져있으니까 어떤식으로든 git 히스토리 정리하시거나 서브모듈로 설정하라는 문구와 저런 아이콘이 생기나보다!
