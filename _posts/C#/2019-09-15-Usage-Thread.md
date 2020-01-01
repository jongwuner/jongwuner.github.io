---


layout: post
comments: true
categories: C#
---

## **Thread란?**



## **다양한 Thread 호출방식**

```C#
class Program
{
    static void Main(string[] args)
    {            
        // Run 메서드를 입력받아
        // ThreadStart 델리게이트 타입 객체를 생성한 후
        // Thread 클래스 생성자에 전달
        Thread t1 = new Thread(new ThreadStart(Run));           
        t1.Start();
            
        // 컴파일러가 Run() 메서드의 함수 프로토타입으로부터
        // ThreadStart Delegate객체를 추론하여 생성함
        Thread t2 = new Thread(Run);
        t2.Start();

        // 익명메서드(Anonymous Method)를 사용하여
        // 쓰레드 생성
        Thread t3 = new Thread(delegate()
        {
            Run();
        });
        t3.Start();

        // 람다식 (Lambda Expression)을 사용하여
        // 쓰레드 생성
        Thread t4 = new Thread(() => Run());
        t4.Start();

        // 간략한 표현
        new Thread(() => Run()).Start();
    }

    static void Run()
    {
        Console.WriteLine("Run");
    }
}
```



## References

1. 스레드 이해 잘되는 예제 :  https://m.blog.naver.com/go4693/221313272712a


2. ParameterizedThreadStart : https://docs.microsoft.com/ko-kr/dotnet/api/system.threading.thread.-ctor?view=netframework-4.8