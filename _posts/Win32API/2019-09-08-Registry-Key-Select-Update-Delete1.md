---
layout: post
comments: true
categories: Win32API
---

## **Registry 란?**

 **레지스트리**란 윈도우계열 시스템에서 사용하는 시스템 구성 정보를 저장한 데이터베이스를 말한다.

 프로세스종류, 주기억장치의 용량, 주변장치의 정보, 시스템 매개변수, 응용소프웨어에서 취급하는 파일 타입과 매개변수 등을 기록한 **저장소**를 말한다.<br>

<br>

![image](https://user-images.githubusercontent.com/16419202/66094385-cd2fdb00-e5ce-11e9-8a5b-5b24792257f5.png)

<br>

### **기본키 5개** 

- **HKEY_CLASSES_ROOT**

  [파일 연결](https://ko.wikipedia.org/w/index.php?title=파일_연결&action=edit&redlink=1), [OLE](https://ko.wikipedia.org/wiki/객체_연결_삽입) 객체 클래스 ID와 같은 등록된 응용 프로그램의 정보를 담고 있다.

- **HKEY_CURRENT_USER**

  현재 로그인한 사용자의 설정을 담고 있다.

- **HKEY_LOCAL_MACHINE**

  컴퓨터의 모든 사용자의 설정을 담고 있다.

- **HKEY_USERS**

  컴퓨터에서 사용 중인 각 사용자 프로파일에 대한 HKEY_CURRENT_USER 키에 일치하는 서브키를 담고 있다.

- **HKEY_CURRENT_CONFIG**

  실행 시간에 수집한 자료를 담고 있다. 이 키에 저장된 정보는 디스크에 영구적으로 저장되지 않고 시동 시간에 생성된다.



![image](https://user-images.githubusercontent.com/16419202/66094451-fe101000-e5ce-11e9-91cf-c9202ed2a67d.png)



### Registry 키 열기 / 닫기

```C++
LONG WINAPI RegOpenKey(
	__in HKEY hKey;
    __in_opt LPCTSTR lpSubKey;
    __out PHKEY phkResult;
);
```

- **hKey** : 열고 싶은 키가 속해 있는 **기본키** 지정한다. 

- **lpSubKey** : 기본 키 이하 나머지 경로를 지정한다. 문자열로 지정하되 타입이 LPCTSTR로 선언되어 있으므로 TEXT("")로 감싸야 한다.
- **phkResult :** 열린 키에 대한 핸들이 여기로 전달된다. **(&hKey)**

**※ 함수 수행 성공 시 ERROR_SUCCESS 매크로 상수를 반환한다.** 



```c++
LONG WINAPI RegCloseKey(
	__in HKEY hKey;
);
```

- phkResult를 닫는 핸들 키이다.



> 사용법

```C++
HKEY hKey;
RegOpenKey(HKEY_LOCAL_MACHINE, TEXT("Software"), &hKey);
RegCloseKey(hKey);
```



## **References**

1. http://blog.naver.com/PostView.nhn?blogId=fablezzg&logNo=10031033283&redirect=Dlog&widgetTypeCall=true

2. 레지스트리 읽기 / 쓰기 : http://zbaekhk.blogspot.com/2011/06/mfc_16.html

3. 레지스트리 서브트리 구성별 : https://m.blog.naver.com/PostView.nhn?blogId=rbdi3222&logNo=220597850076&proxyReferer=https%3A%2F%2Fwww.google.com%2F
4. 레지스트리 위키 : [https://ko.wikipedia.org/wiki/%EC%9C%88%EB%8F%84%EC%9A%B0_%EB%A0%88%EC%A7%80%EC%8A%A4%ED%8A%B8%EB%A6%AC](https://ko.wikipedia.org/wiki/윈도우_레지스트리)