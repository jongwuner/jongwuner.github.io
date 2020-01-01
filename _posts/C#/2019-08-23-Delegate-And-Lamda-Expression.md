---
layout: post
comments: true
categories: C#
---

[TOC]

## Delegate와 익명메소드

- 익명 메소드란 이름이 없는 메소드이다.
- 한 번 사용하고 다시 사용할 일이 없을 것 같으면 익명메소드로 사용하는 것이 낫다.



> Delegate 선언

```C#
delegate int Calculate(int a, int b);
```



>메인

```C#
static void Main()
{
	Calculate calc1, calc2;
    calc1 = delegate(int x, int y){return x + y;};
    calc2 = (x, y) => {return x - y};
    
    Console.WriteLine(calc1(5, 6));
    console.WriteLine(calc2(5, 6));
}
```







## References

1. Invoke : https://docs.microsoft.com/ko-kr/dotnet/api/system.windows.forms.control.invoke?view=netframework-4.8
2. MethodInvoker : http://www.masque.kr/free/383086

