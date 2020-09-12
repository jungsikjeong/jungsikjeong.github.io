---
layout: post
title: github Pages 배포
category: memo
tags: [memo]
comments: true
---

# github Pages 배포

> [참고자료:노마드코더](https://nomadcoders.co/nwitter/lectures/1935)

## github를 이용한 배포 방법

- npm i gh-pages
- package.json 맨 하단부분에 `"homepage": "https://[유저이름].github.io/[저장소이름]"` 작성
- scripts 부분에 "predeploy": "npm run build", "deploy": "gh-pages -d build" 작성
- 이후 `npm run deploy` 해주면 됨

```
// package.json
{
  "name": "nwitter",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "@fortawesome/fontawesome-free": "^5.14.0",
    "@fortawesome/fontawesome-svg-core": "^1.2.30",
    "@fortawesome/free-brands-svg-icons": "^5.14.0",
    "@fortawesome/free-regular-svg-icons": "^5.14.0",
    "@fortawesome/free-solid-svg-icons": "^5.14.0",
    "@fortawesome/react-fontawesome": "^0.1.11",
    "@testing-library/jest-dom": "^4.2.4",
    "@testing-library/react": "^9.3.2",
    "@testing-library/user-event": "^7.1.2",
    "firebase": "^7.19.1",
    "react": "^16.13.1",
    "react-dom": "^16.13.1",
    "react-router-dom": "^5.2.0",
    "react-scripts": "3.4.3",
    "uuid": "^8.3.0"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "eject": "react-scripts eject",
    "predeploy": "npm run build",
    "deploy": "gh-pages -d build"
  },
  "eslintConfig": {
    "extends": "react-app"
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  },
  "homepage": "https://jungsikjeong.github.io/nwitter"
}
```
