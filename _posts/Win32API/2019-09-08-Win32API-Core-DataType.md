---
layout: post
comments: true
categories: Win32API
---

## **주로 등장하는 자료형**

- HKEY

- TCHAR

  ```
  #include <tchar.h>
  #define _UNICODE    // ==> TCHAR를 wchar_t 형으로 대치
  #define _MBCS       // ==> TCHAR를 char 형으로 대치 (default)
  ```

  자신의 운영체제가 multi-byte환경이면, char형으로,
  unicode환경이면, w_char, wide char형으로 type casting됩니다.

- LPTSTR  

  - LP: Long Pointer
  - C : Const 상수
  - STR : 문자열. 뒤에 ''\0'
  - TSTR : t_char
  - W : wide ==> w_char

- DWORD

- __T, L""

- 유니코드 vs 멀티코드

- **LPBYTE :** 

## **References**

- https://m.blog.naver.com/PostView.nhn?blogId=feelwoo&logNo=100036706623&proxyReferer=https%3A%2F%2Fwww.google.com%2F

- 자료형에 대한 깔끔한 정리 : http://pelican7.egloos.com/v/1768951