---
layout: post
comments: true
categories: OS
---

### Regedit.exe 실행후

<br><br>

### 32bit || 64bit Dir: <br>

*HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Windows* 에서

1. `AppInit_DLLs` 에 경로 설정
2. `LoadAppInit` value = 1

<br>

### 64bit Dir:<br>

*HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Windows*에서<br>

1. `AppInit_DLLs`에 경로설정
2. `LoadAppInit` value = 1<br><br><br><br>