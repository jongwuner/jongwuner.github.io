---
layout:     post
title:      "[데일리 러브미션(1)] Node.js기반 카카오톡 챗봇서비스 만들기"
subtitle:   "프로젝트 개요"
date:       2020-03-22 03:34:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: Project
tags:
  - Node.js
  - React
---

![image](https://user-images.githubusercontent.com/16419202/77233828-85892400-6bed-11ea-86fd-ddc1d619783b.png)
데일리 러브미션의 초라한 v1.0.0버전.. 하지만 나는 내가 운영자인 마냥 이렇게 행세하는 것이 어린 시절에 소꿉놀이하는 것 처럼 즐겁다.
<br>
## 왜 하는가??
J님과 대화를 하던 도중, 우리는 서로가 너무 다르다는 것을 깨달았다. (..슬픈 주제가 아니다.)<br>
둘다 취업, 수험을 앞두고 있는 처지인데 가장 중요한 것이 `동기부여` 라는 키워드이다. <br>
근데 J님과 나는 `동기부여` 에 대해서 바라보는 관점이 조금은 다르다. <br>
나는 순수한 동기부여가 조금 되는 편이다. 좋은점이라고 할 수도 있지만 스스로 생각했을 때<br>
조금 과할 때가 있다. 세상에 존재하는 소프트웨어는 혼자 다 만들 것 처럼(?) 행세할 때가 있다.<br>
반면 J님은 학생들에게 '교육의 진정한 의미를 깨닫게 해주는 교사가 될거야'라는 식의 동기부여와는<br>
거리가 많이 멀다. 그저 조금은 단순한 동기. 그저 내가 해오던 것이며, 이게 제일 나랑 잘 맞는다. <br>
약간 그냥 한다? 라는 느낌. 사실 처음에는 이런 J님을 걱정 많이 했었는데, 똑똑해서 내가 걱정할<br>
수준은 절대 아니란 것을 깨달았다. <br>
<br>
<br>
서론이 너무 길었는데 순수한 동기부여보다는 이번주 공부를 열심히 햇으니 주말엔 야식을 먹어야지!<br>
식의 동기부여가 더 와닿는 다는 점에 착안해서, 내가 도울 수 있는게 없을까? 라는 생각을 하게 되었다.<br>
하루 목표를 달성하면 도장찍는 식의 어플을 추천해주려고 하다가 마땅한게 없다는 것을 깨달았다. <br>
`챌린저스` 라는 비슷한 목표의 도전자들끼리 펀딩을 하는 현금동기부여 앱이 있었는데, <br>
우리 둘의 각기 다른 하루의 목표를 통해 경쟁하는 방식으로 앱을 만들어보고 싶다는 생각이 들었다.<br>
그리고 나의 개발자능력을 J님께 인정받아 내가 공부하는 것을 인정받고 싶기도 했다.<br>
<br>
![image](https://user-images.githubusercontent.com/16419202/75858592-e10c9100-5e3b-11ea-9d71-0a7eaa2fb6c7.png)
## 아이디어 기획
바로 아이디어 설계를 해보기 시작했다. 충동적으로<br>
### 로고
일단 위에 로고부터 만들기 시작했는데 고민의 결과라기 보다는 그냥 이런 건 끄적이면서 나오는 부분이지
이런 로고를 만들면 뭔가 진짜 열망이 들끓는달까, 진짜 내가 서비스를 하는 느낌?
<br>
### Backend(Node.js)
즉각적으로 한번 만들어보기 위해 가장 먼저 떠오른건 Node.js의 빠른 생산성이다. Express 때려박으면 일도 아닐것같았다. <br>
요즘 System-monitor 프로젝트때문에 묵혀뒀던 Node.js를 구글링하기 시작했다. <br>

### 챗봇(Python, Kakao Open Builder)
req가 이미지라는 것을 전제로 하고, 시간이 07:00이전, 23:00이전이라고 설정을 해두면, 그 시간에 전송되는 이미지를 저장해두고, 
웹사이트에서 순차적으로 저장을 하고, 컨트리뷰션 그래프를 색칠한다! 그리고 response를 챗봇으로 반응하게끔 시킨다.
그리고 해당날의 00시에 미션수행결과를 채널로 전송한다!

### Front-end(React.js, kakaotalk)
React.js를 사용하는 지점은 웹사이트가 구현되었을 때, 그리고 컨트리뷰션 그래프도 react로 구현한다. 구현의 속도를 올리기위해
react 템플릿을 좀 구해보면 좋을 듯하다.

### 추후 포스팅 계속 ~~