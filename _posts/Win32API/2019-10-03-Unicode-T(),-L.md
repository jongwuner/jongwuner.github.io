---
layout: post
comments: true
categories: Win32API
---

# **GetSystemInfo(&sysInfo);**

> GetSystemInfo의 구조

```C++
typedef struct _SYSTEM_INFO{
    union{
        DWORD dwOemId;			// Obsolete field... do not use
    }
    struct{
        WORD wProcessorArchitecture;
        WORD wReserved;
    } DUMMYSTRUCTNAME;
    DWORD dwPageSize;
    
    LPVOID IpMinimumApplicationAddress;
    LPVOID IpMaximumApplicationAddress;
    
    DWORD_PTR dwActiveProcessorMask;
    DWORD dwNumberOfProcessors;;
    DWORD dwProcessorType;
    DWORD dwAllocationGranularity;
    
    WORD wProcessorLevel;
    WORD wProcessorRevision;
} SYSTEM_INFO, *LPSYSTEM_INFO;
```



>설명 

- dwOemId
- dwPageSize
- dwActiveProcessorMask
- **dwNumberOfProcessors :** CPU의 스레드 갯수임. (CPU의 코어개수 X)
- **dwProcessorType**
  - PROCESSOR_INTEL_386 (386)
  - PROCESSOR_INTEL_486 (486)
  - PROCESSOR_INTEL_PENTIUM (586)
  - PROCESSOR_INTEL_IA64 (2200)
  - PROCESSOR_AMD_X8664 (8664)
  - PROCESSOR_ARM (Reversed)
- dwAllocationGranularity
- wPProcessorArchitecture
- wReversed
- wProcessorLevel
- wProcessorRevision



# PDH(Performance Data Helper)

> PC의 현재 CPU 사용량 

```C++
#pragma comment(lib, "pdh.lib")

#include "TCHAR.h"
#include "pdh.h"
#include<iostream>
using namespace std;

static PDH_HQUERY cpuQuery;
static PDH_HCOUNTER cpuTotal;

void init() {
	PdhOpenQuery(NULL, NULL, &cpuQuery);
	PdhAddCounter(cpuQuery, L"\\Processor(_Total)\\% Processor Time", NULL, &cpuTotal);
	PdhCollectQueryData(cpuQuery);
}

double getCurrentValue() {
	PDH_FMT_COUNTERVALUE counterVal;

	PdhCollectQueryData(cpuQuery);
	PdhGetFormattedCounterValue(cpuTotal, PDH_FMT_DOUBLE, NULL, &counterVal);
	return counterVal.doubleValue;
}

int main() {
	init();
	while (true) {
		cout << "USAGE : "<< getCurrentValue() << "\n";
		Sleep(500);
	}
	return 0;
}
```







# Reference

1. 코어개수 : https://neodreamer-dev.tistory.com/605

2.  http://x108zero.blogspot.com/2013/12/text-t-l.html

3. 멀티바이트, 유니코드

4. PDH(Performance Data Helper)

   - 

   - 윈도우즈 환경에서는 PDH(Performance Data Helper) 라이브러리를 이용해, [성능 카운터 정보](http://serious-code.net/doku/doku.php?id=kb:windowsperformancecounter)를 쉽게 알아낼 수 있다. 서버 프로그램에다 이 기능을 집어넣고, 통계를 파일에다 기록해두면, 나중에 뭔가 눈에 보이지 않는 문제가 생겼을 때 대처할 수 있는 근거 자료가 된다.
   - http://serious-code.net/doku/doku.php?id=kb:windowsperformancecounterusingcpp
   - pdh를 활용해서 mem, cpu사용량 : [https://wyseburn.tistory.com/entry/pdhh-%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-CPU%EB%A9%94%EB%AA%A8%EB%A6%AC-%EC%82%AC%EC%9A%A9%EB%9F%89-%ED%99%95%EC%9D%B8-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-%EB%8D%B0%EB%AA%A8](https://wyseburn.tistory.com/entry/pdhh-를-이용한-CPU메모리-사용량-확인-라이브러리-데모)

5. ULARGE_INTEGER : 용량이 커서 integer로는 해결이 안되기떄문

   1. https://m.blog.naver.com/PostView.nhn?blogId=lhk0523&logNo=140153391828&proxyReferer=https%3A%2F%2Fwww.google.com%2F