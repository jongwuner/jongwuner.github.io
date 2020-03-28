---
layout:     post
title:      "system-monitor 서버구현기 - [Android, Spring-boot, Swing TEST"
subtitle:   "Async-Long-Polling Server Based Spring-boot"
date:       2020-03-28 04:01:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: web
tags:
  - Spring-boot
---

![image](https://user-images.githubusercontent.com/16419202/77831675-f68f8500-7173-11ea-953f-d796ad884a05.png)

## 시작부터 삐걱(AWS Issue)
![image](https://user-images.githubusercontent.com/16419202/77831720-2ccd0480-7174-11ea-9f6d-8287f52608b4.png)
나의 징징거림으로부터 `2020-03-28` 의 회의가 시작되었다. AWS 계정의 주인인 다민이와 실질적인 EC2 운영을 하는 나의 관계는 참
뗄레야 뗄수가 없다. Xshell을 통해서 우리서버 22번포트에 접속을 하면 가끔 `RSA key`가 갑자기 바뀌는 현상이 종종 있었다.
원인을 아직까지 알 순 없지만, 내가 추측하는 문제는 일단 몇 가지가 있다. <br>
<br>
1. server에 접속을 오랫동안 하지 않아서?
2. `system-monitor.war` 이 EC2에 과부하를 줘서?
<br>
이 정도인데,, 정확히는 아직도 파악 중이다. 이 문제로만 회의를 40분가량 사용했다. 
![image](https://user-images.githubusercontent.com/16419202/77831918-72d69800-7175-11ea-830e-7eda599d2cb2.png)

## Issue 해결의 성과
![image](https://user-images.githubusercontent.com/16419202/77831989-0f009f00-7176-11ea-92ee-ae8d908d3d42.png)
<br>
가장 큰 문제였던<br>
1. Android 에서 종료예약이 되지 않았던 점.
2. Server에서 extension 처리가 제대로 되지 않았던 점.
- Local에서는 잘 작동하고, AWS에서는 잘 안된다고 인지했던 그 문제.
<br>
이 2가지 사항이 잘 해결되고, 나서 술술 풀렸다.  또 다른 `Unable to 6379(Redis)` To-do를 맞이했지만, 밤샘코딩을 통해 해결을 했다.
이 문제는 아마 syncCmd 방식으로 redis-server에 접근해서 발생하는 문제같다. 
![image](https://user-images.githubusercontent.com/16419202/77832113-f47af580-7176-11ea-9051-f76a050e0227.png)
위 사진 처럼 Warning Message가 계속 뜨는 것을 볼 수 있는데, close를 하면 이미 연결이 끊겨있다는 문구를 볼 수 있다. 비동기적으로 작동하는 로직에서 `getConnectionExit()`이 상황에 맞지 않게 호출된다는 것을 알 수 있었다. 
해결책은 우선 `Thread.sleep()`으로 해결했지만, Thread.sleep을 남용하면 코드가 아름답지(?) 않기에 다른 방법을 한번 강구해보겠다.
- `asyncCmd`
- `synchronized(lock)`

## 다음주 계획
팀원들이 재학생이어서 일단 캡스톤 수업에 system-monitor 프로젝트를 제출한다고 들었다. 그래서 ver3~ver4에 대한 구체적인 설계를 한번 진행해볼 예정이다.