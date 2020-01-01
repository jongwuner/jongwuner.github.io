---
layout: post
comments: true
categories: Hooking
---



<br>

#### User Mode Hooking<br>

- IAT Hooking
- Trampoline Code Hooking
- EAT Hooking

> 정리

1. `API Function` 의 실행흐름에서 제어권을 가져오는 방법
   - 0xCC, JMP Code, IAT, EAT Patch
2. 제어권을 가져온 후 원하는 동작을 하기 위한 방법
   - DLL Injection, Debugger Attach

<br>

#### Kernel Mode Hooking<br>

- SSDT Hooking(System Service Descriptor Table)
  - Native API 주소를 보관하고 있는 테이블
- IDT Hooking (Interrupt Descriptor Table)
  - 인터럽트 핸들러 주소를 보관하고 있는 테이블
- IRP Hooking

