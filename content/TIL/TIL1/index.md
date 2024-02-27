---
emoji: ✍
title: 기록1
date: '2023-11-01 20:36:00'
author: 정중식
tags: TIL
categories: TIL
---

## 23.11.01

- 모던 자바스크립트 공부/코드 품질 파트 완독

  코드 품질 파트에서 `닌자 코드`섹션이 인상 깊었다.
  변수명 혹은 함수명을 어떤식으로 작명하면 안되는지를 유머러스하게 설명하는데 재밌었다.

- 팀 프로젝트 `Read A Perfume` 개발

  - 카테고리 공통 컴포넌트 개발<br/>

    팀 프로젝트에서 내가 맡은 분야는 제품 리스트 페이지와, 제품 상세 페이지인데
    제품 리스트 페이지에 들어가는 카테고리와 메인 페이지에 들어가는 카테고리가 겹치는것 같아서 카테고리 컴포넌트를 따로 만들어서 공통적으로 사용할 수 있게끔 해주었다.<br/>

  - 제품 상세 페이지 UI 및 css 작업

    오늘 작업한 페이지!

![사진](./til1.gif)

> 코드 구조를 생각하면서 하다보니까 뭔가 작업속도가 더딘것 같다..

## 23.11.02

- 팀 프로젝트 제품 상세페이지 UI 및 css 작업

  - 향수의 특징을 react-apexcharts 라이브러리를 사용해 레이더 차트로 표시해주었다.

  - 사용자가 좀 더 정확하게 향수의 특징을 볼 수 있도록 materialUI의 아코디언 메뉴를 사용해서 향수의 특징을 막대차트화 해주었다.

  > 이런식으로..

  ![사진](./til2.gif)

  여기서 문제는, 해당 차트의 화살표를 클릭해서 펼치면 이쁘게 딱 나오지 않는다는거다.
  디자이너분께서 짠 구조는 이런식인데..

  ![사진](./이런식.png)

  나는 누르면 이렇게 나온다.

  ![사진](./누르면이렇게.png)

  마우스 오른쪽을 클릭해서 html,css 구조를 살펴봤는데 마진값,패딩값이 주어져있는게 아니라
  div태그 두개로 요소가 나누어져있었다.

  포지션 앱솔루트를 줘서 당겨주면 어떨까? 싶어서 시도해봤다.

  ![사진](./누르면이렇게.gif)

  디자인대로 됬지만, 열고 닫을때 매끄럽지가 않았고, 계절 아코디언 같은 경우 봄 차트의 마진이 좀 깨졌다.
  (포지션 앱솔루트와는 별개인듯하다. 한글자 css처리를 따로 해줘야할듯 싶다.)

- 방법을 찾던 중 UI적으로 좀 불편해보인다는거를 깨달았다.
  아코디언 탭을 누르기전에는 가장 순위가 높은 차트를 아코디언 제목으로 보여주고,
  아코디언 탭을 누르면 가장 순위가 높은 차트를 포함한 전체 순위의 그래프차트를 보여주는 방향으로 적용시켜봤다.

  ![사진](./최종.png)

> 근데 또 생각해보니까 디자인대로하는게 베스트인거같은데..

## 23.11.03

- 팀 플젝 UI 및 css 작업

  아코디언 메뉴를 살펴봤다..

## 23.11.04~06

컨디션이 안좋아서 휴식했다.

> 휴식은 게으름도, 멈춤도 아니다.
> 휴식을 모르는 사람은
> 브레이크가 없는 자동차 같아서
> 위험하기 짝이 없다. -헨리 포드-

```toc

```