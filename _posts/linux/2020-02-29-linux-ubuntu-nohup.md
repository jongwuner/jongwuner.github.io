---
layout: post
title: "[Linux, Ubuntu] nohup로 프로세스 켜기/끄기"
subtitle: '서버pc가 종료되어도 프로세스 지속시키는 방법'
author: "jjongwuner"
header-style: text
tags:
  - linux
  - vim
---

`AWS`를 주로 사용하시는 유저들에게 정말 큰 꿀팁이 될 것이라고 생각한다. 
서버 PC로 이용해야하는 Linux/Ubuntu에게는 꼭 필요한 기능이 `nohup`이다.

### nohup을 통해 프로세스 켜기 (서버 종료되어도 지속됌.)

`nohup & [program Dir]` 


### nohup로 실행된 프로세스 끄기

`ps -ef | grep [Process Name]`  <--- 실행중인 pid를 얻는다.   
`kill -9 [Pid]` <--- pid를 입력하여 프로세스를 종료시킨다.






