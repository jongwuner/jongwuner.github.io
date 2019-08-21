---
layout: post
comments: true
categories: OS
---

\- 함수 원형<br>

 

![img](https://mblogthumb-phinf.pstatic.net/20150330_209/wkdghcjf1234_14276986647341fJUS_PNG/%C4%B8%C3%B3.PNG?type=w2)

 <br>

 인수가 하나 뿐입니다. 이 인수로 어느 특정한 핸들(HANDLE)을 닫습니다.<br>

 <br>

 이 함수의 반환형은 BOOL 입니다. 성공적으로 핸들을 닫았을 경우 FALSE(0)가 아닌 값, 실패했을 경우 FALSE(0)를 반환합니다.<br><br><br>

 \- 부가 설명<br>

 <br><br>

 이 함수는 어느 특정한 핸들을 닫습니다. 단, 그 특정한 핸들에 윈도우 핸들([HWND](http://wkdghcjf1234.blog.me/220250185961))과 각종 GDI 핸들은 포함되지 않습니다.<br><br>

 <br>

 특정 함수를 통해 특정 핸들을 발급받은 경우 그 핸들은 메모리 공간을 차지합니다. 이 함수 또는 다른 핸들 닫기 함수를 통해 핸들을 닫지 않으면 메모리 누수가 발생할 수 있습니다.<br><br><br>

 

 핸들을 닫는다고 해서 그 핸들과 연결된 실제 객체가 종료되는 것은 아닙니다. 예를 들어, 스레드 핸들을 닫는다고 해서 스레드가 종료되는 것은 아닙니다.<br><br>

 

 응용 프로그램이 디버그 모드로 실행되었을 경우 유효하지 않은 핸들 값을 전달하였을 경우 함수는 예외를 발생시킵니다. 응용 프로그램이 디버그 모드가 아닐 경우 ERROR_INVALID_HANDLE 값을 반환합니다.<br><br><br>

 

 함수가 실패하였을 경우 GetLastError 함수를 통해 오류를 조회할 수 있습니다.<br><br><br>

 

 

 \- 참조<br><br><br>

 

 이 함수를 통해 닫을 수 있는 핸들의 유형은 다음과 같습니다.<br>

 <br><br>

Access Token<br>

Communications Device<br>

Console Input<br>

Console Screen Buffer<br>

Event<br>

File<br>

File Mapping<br>

Input/Output Completion Port<br>

Job<br>

Mail Slot<br>

Memory Resource Notification<br>

Mutex<br>

Named Pipe<br>

Pipe<br>

Precess<br>

Semaphore<br>

Thread<br>

Transaction<br>

Waitable Timer<br>

 <br><br>

 

 \- 헤더 파일<br>

 Winbase.h (Windows.h 파일에 포함되어 있음.)<br><br>

 \- 라이브러리 파일<br>

 Kernel32.lib<br><br>

 \- 동적 연결 라이브러리(.dll)<br>

 Kernel32.dll<br><br>

