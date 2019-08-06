---
layout: post
comments: true
categories: Hooking
---

![tecmap](https://github.com/jongwuner/Etc/blob/master/Hooking/img/Hooking%20TecMap.PNG)

# Classification for API hooking methods.

The API hooking method divides into `a static method` and `a dynamic method` largely depending on an object to be worked on.

**The static method** is based on the assumption that the object to be processed.
**The dynamic method** is to work with 'memory'.

Common API hooking is dynamic.

| Category              | dynamic                    | static                          |
| --------------------- | -------------------------- | ------------------------------- |
| Destination           | File                       | Memory                          |
| Hooking time          | Before running the program | After running the program       |
| When to Use           | Special Situations         | General Hooking                 |
| Terminate the program | terminate for unhook       | unhook during program execution |

<br><br>

# Location

How to change the API address in the 'IAT' to the hooking function address.
The advantages are simple, and the easiest to implement.
The disadvantage is that it is not in the 'IAT' but you can not hook the APIs used in the program.<br>
(Eg APIs that dynamically load and use DLLs)

## Code

It is a method of searching the actual address of the API in the system library (* .dll) mapped to the process memory and directly modifying the code.
Note that this is the most widely used method, and there are a variety of options for implementation:

> > How to patch the first 5 bytes with the JMP XXXXXXX command<br>
> > How to overwrite part of a function<br>
> > How to make some changes to just the parts you need<br>

## EAT

It is a method to change the start address of the API recorded in the EAT (Export Address Table) of the DLL to the hooking function address. The concept is simple, but the **2)**method in the code implementation is simpler and more powerful, so the EAT modification method is not used well.

<br><br>

# Technique (How)

This is a concrete technique for penetrating memory and installing hooking functions.
Debug and Injection methods are divided into two parts. Injection method is divided into Code and Dll methods.

## Debug

How to hook API while debugging the target process.
Since Debugger has full control over Debuggee (Execution Control, Memory Access, etc.), Debugger's process memory
Hooking functions can be freely installed.

The Debugger is not a typical ``OllyDbg, Windbg, or IDAPro``, but is a user-created program for hooking.
That is, it attaches to the target process using the Debug API in the program, and installs the hooking function (the execution stops temporarily). After that,
Resuming execution will result in complete API Hooking.

There is, of course, a way to automate API hooking by using automation scripts in existing debuggers (OllyDbg, Windbg, and IDAPro). Especially Immunity Debugger
In the same case, it supports powerful dedicated Python scripts.



## Injection

Injection technique is a technology that penetrates the corresponding process memory area. 1) Code injection
2) It can be divided into DLL Injection. Among them, the DLL Injection technique is most widely used.

- DLL Injection is a technique that forces the target process to load the DLL file that the user wants.
  If hooking code and installation code are created in advance in DLL to be injected and installation code is called from DllMain (), API hooking is completed at the moment of injection.
- Code Injection technique is a more advanced (complex) technology than existing DLL Injection, mainly used in malicious code (virus, shellcode, etc).
  (DLL Injection is a good detection of AV products, malicious code is more difficult to detect more Code Injection is trying.)

The Code Injection technique is very difficult to implement. The reason for this is not the complete PE image like DLL Injection, but only executable code and data
Injection requires that you obtain and use the necessary API address yourself, and be very careful not to access the wrong address when accessing the memory address in the code.