---
layout:     post
title:      "Spring에서 Observer Pattern으로 비동기 스레드에 알림주기"
subtitle:   "Async-Long-Polling Server Based Spring-boot"
date:       2020-03-03 04:01:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: web
tags:
  - Web
  - Spring-boot

---

## Observer과 Observable

## Observable Code
```java
public class 책끝을접다 implements Observable {

    List<Observer> observerList = new ArrayList<>();

    private boolean Pc사용시간변경;

    public boolean isPc사용시간변경() {
        return Pc사용시간변경;
    }

    public void 신규컨텐츠나왔다() {
        System.out.println("PC/Mobile로 부터 Pc사용종료 명령이 들어왓습니다.");
		신규컨텐츠등록 = true;
        구독자들에게알리기();
    }

    @Override
    public void 구독하기(Observer o) { // 새로 켜지는 PC들
        observerList.add(o);
    }

    @Override
    public void 구독해지(Observer o) { // 꺼지는 PC들
        observerList.remove(o);
    }

    @Override
    public void 구독자들에게알리기() {
        observerList.forEach(Observer::업데이트); // 사용종료가 신청된 Pc id와 endTime 보내주기.
    }
}
```

### Observer Code
```java
public class DaminPc implements Observer {

    @Override
    public void 업데이트() {
        System.out.println("라이언: 책 끝을 접다 재밌다!");
    }
}
```
```java
public class jjongwunerPC implements Observer {

    @Override
    public void 업데이트() {
        System.out.println("무지: 콘한테 책 끝을 접다 공유해야지!");
    }
}
```

### Main Code
```java
페이지 책끝을접다 = new 페이지("책끝을접다");
Observer 라이언 = new 구독자("라이언");
Observer 무지 = new 구독자("무지");

책끝을접다.구독하기(라이언);
책끝을접다.구독하기(무지);

책끝을접다.신규컨텐츠나왔다();

책끝을접다.구독해지(무지);

책끝을접다.신규컨텐츠나왔다();
```
<br><br>
```java
MobileObservable 모바일모니터 = new 클라이언트("Mobile");
PcObservable 컴퓨터모니터 = new 클라이언트("Pc");
Observer DaminPc = new 구독자("Damin");
Observer jjongwunerPc = new 구독자("jjongwuner");

모바일모니터.구독하기(jjongwunerPC);
컴퓨터모니터.구독하기(daminPC);

모바일모니터.종료변경감지(jjongwunerPC, 2020-03-03-04-34);
컴퓨터모니터.종료변경감지(DaminPc, 2020-03-03-06-40);

//jjongwunerPC. PowerStatus : OFF 반환시
모바일모니터.구독해지(jjongwunerPC);
컴퓨터모니터.구독해지(jjongwunerPC);

//DaminPC. PowerStatus : OFF 반환시
모바일모니터.구독해지(DaminPC);
컴퓨터모니터.구독해지(DaminPC);

```
## Main Code Result
```
모바일에서 jjongwunerPC 에게 종료시간변경신청이 들어왔습니다. [ 2020-03-03-04-34 ]
컴퓨터에서 DaminPC에게 종료시간변경신청이 들어왔습니다. [ 2020-03-06-40 ] 


```

## References
- [ Java Thread Search By ID and Interrupt](https://stackoverflow.com/questions/26213615/terminating-thread-using-thread-id-in-java)
- [ Java Thread Search](https://stroot.tistory.com/53)
- [ Java Observer Pattern in Thread](https://stackoverflow.com/questions/36773867/how-do-i-implement-observer-design-pattern-for-a-multi-threaded-java-server)
- [ Java Observer Pattern - 2](https://victorydntmd.tistory.com/296)
- [ Java Observer Pattern - 1](https://futurecreator.github.io/2018/06/04/java-observer-pattern/)