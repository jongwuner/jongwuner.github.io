---
layout:     post
title:      "Spring에서 Async로 Rest-ful 메소드 구현하는 방법"
subtitle:   "Async-Long-Polling Server Based Spring-boot"
date:       2020-01-02 21:20:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: web
tags:
  - Web
  - Spring-boot

---

## Async를 이해하기전, 선행지식 몇 가지
.
- 먼저 람다식(Lamda Expression)에 대한 문법이해가 부족하다면, 이 글부터 읽기를 바란다. 
  - [람다식에 대한 이해]()
- Callback 함수 : callee가 caller에게 정보를 전달하는 방식.
  - [Callback함수의 개념과 예제]()
- Runnable 함수와 Callable의 차이
  - [Runnable 함수 vs Callable 함수]

## Async란?


## References
- [Callable method](https://bkim.tistory.com/3)
- [Java Callback 예시 - 3](https://brunch.co.kr/@kimkm4726/1)
- [Java Callback 예시 - 2](http://www.dreamy.pe.kr/zbxe/CodeClip/3768942)
- [Java Callback 예시 - 1](https://devsophia.tistory.com/entry/JAVA-%EC%BD%9C%EB%B0%B1-%EB%A9%94%EC%84%9C%EB%93%9C-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0)
- [OkHttpClass](https://digitalbourgeois.tistory.com/59)
- [Stackoverflow - 2 : callback](https://stackoverflow.com/questions/40311808/how-to-test-rest-endpoint-when-using-callbacks-using-java)
- [Stackoverflow - 1](https://stackoverflow.com/questions/52876489/java-rest-api-post-return-future)
- [AOP , Proxy , Wrapping Object](https://sa1341.github.io/2019/05/25/%EC%8A%A4%ED%94%84%EB%A7%81-AOP-%EA%B0%9C%EB%85%90-%EB%B0%8F-Proxy%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EA%B5%AC%EB%8F%99%EC%9B%90%EB%A6%AC/)
- [AsyncRestTemplate](http://wonwoo.ml/index.php/post/903)
- [AsyncRest](https://www.hungrydiver.co.kr/bbs/detail/develop?id=2&scroll=comment)
- [비동기식 응답지연서버를 만들 수 있는 단서](https://bkim.tistory.com/3)
- [Runnable vs Callable](https://codechacha.com/ko/java-callable-vs-runnable/)
- [람다식과 runnable 예제](https://coding-factory.tistory.com/265)
- [CompletableFuture](https://brunch.co.kr/@springboot/267)