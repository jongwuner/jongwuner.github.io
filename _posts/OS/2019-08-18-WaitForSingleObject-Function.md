---
layout: post
comments: true
categories: OS
---

```
DWORD WINAPI WaitForSingleObject(
  _In_ HANDLE hHandle,
  _In_ DWORD  dwMilliseconds
);
```

 <br>

커널 오브젝트의 상태정보를 확인하는데 사용됩니다.<br>

<br>

**hHandle**<br>

  상태확인을 원하는 커널오브젝트의 핸들을 인자로 전달합니다.<br>

<br>

**dwMilliseconds**<br>

  커널오브젝트가 Singaled상태가 될때까지 기다릴 수 있는 최대 시간입니다.<br>

  만약 상수 INFINITE를 인자로 전달하면 커널 오브젝트가 Signaled 상태가 될 때까지<br>

  반환하지 않고 무한정 기다립니다.<br>

 <br><br>

**반환값**<br>

- *WAIT_OBJECT_0*  -  커널 오브젝트가 Signaled 상태가 되었을 때 반환되는 값<br>

- *WAIT_TIMEOUT*  -   커널 오브젝트가 Signaled 상태가 되지 않고, dwMilliseconds 로 설정한 시간이 넘음<br>

- *WAIT_ABANDONED* - 소유관계와 관련하여 함수가 정상적이지 못한 오류 발생에 의해서 반환되는경우.<br>



https://cinrueom.tistory.com/66

