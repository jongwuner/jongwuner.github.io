---
layout: post
comments: true
categories: ReactJS
---



## **고객정보를 삭제하는 방식**

1. 실제로 DB안에서 삭제를 하는 방식
2. DB 인스턴스를 삭제했다고, 기록하는 방식<br>

<br>

이번 프로젝트에서는 2번으로 진행을 하겠다. 2번으로 진행해야, 데이터가 언제 삭제되었는지 등의 정보를 알 수 있기 때문.

## **DB 테이블 변경**

> 테이블 구조 변경

![1567339309270](C:\Users\jklh0\AppData\Roaming\Typora\typora-user-images\1567339309270.png)

```mysql
ALTER TABLE CUSTOMER ADD createdDate DATETIME;
ALTER TABLE CUSTOMER ADD deletedDate DATETIME;
ALTER TABLE CUSTOMER ADD isDeleted INT;
```

이 프로젝트에서는 편의상 `createdDate`,` isDeleted` 변수만 사용하기로 한다.

> createDate와 isDeleted에 들어있는 NULL값들을 채워준다

![1567339609295](C:\Users\jklh0\AppData\Roaming\Typora\typora-user-images\1567339609295.png)

편의상 이미 만들어졌던 인스턴스들은 createDate를 현재시간으로 넣어주고, isDeleted는 0으로 채워준다.



![1567339780688](C:\Users\jklh0\AppData\Roaming\Typora\typora-user-images\1567339780688.png)



## References****

1. **Material-ui** : https://material-ui.com/demos/tables/
2. 동빈나 Youtube : https://www.youtube.com/watch?v=YO9CqrnxbFU&list=PLRx0vPvlEmdD1pSqKZiTihy5rplxecNpz&index=6