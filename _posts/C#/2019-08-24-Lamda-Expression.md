---


layout: post
comments: true
categories: C#
---

## **람다식이란?**

람다식은 **무명메소드를 단순한 계산식**으로 표현한 것이다.<br>

메소드는 매개변수, 내부식, 반환형으로 구성되어 있는데, 이 세 개를 가지고 메소드를 계산식으로 표현한다.<br>

```C#
MyDelegate A;

// 무명 메소드
A = delegate(int a, int b)
{
	return a + b;
}
```

```C#
MyDelegate A;

// 람다식
A = (int a, int b) => a+b;

// 동일한 람다식
// A = (a, b) => a+b;
```

### **예제**

무명 메소드에 비해 상당히 간결하게 표현되는 것을 확인할 수 있다. <br>

람다식은 매개변수로 전해지는 a, b의 타입까지도 생략이 가능하다. <br>

```C#
class MainApp
{
	delegate int MyDelegate(int a, int b);
    
    delegate void MyDelegate2();
    
    static void Main(string[] args)
    {
    	MyDelegate add = (a, b) => a+b;
        MyDelegate2 lamda = () => Console.WriteLine("람다식");
        
        Console.WriteLine("11 + 22 = {0}", add(11, 22));
        
        lamda();
    }
}

Result:
11 + 22 = 33
람다식
```



<br><br><br>



## **람다식의 다양한 활용**

람다식은 단순한 계산식 하나만을 표현하였다. <br>

람다식은 단순한 계산식 하나뿐 아니라 여러가지 처리도 가능하다.<br>

```C#
delegate void MyDelegate(int a, int b);

MyDelegate A = (a, b) => 
{
	if(a > b)
        Console.WriteLine("{0}가 크다", a);
    else if(a < b)
        Console.WriteLine("{0}가 크다", b);
    else
        Console.WriteLine("{0}, {1}는 같다.", a, b);
};
```

### **예제**

```C#
class MainApp
{
 	delegate void MyDelegate(int a, int b);
    
    static void Main(string[] args)
    {
     	MyDelegate Compare = (a, b) =>
        {
            if(a > b)
                Console.WriteLine("{0}보다 {1}가 크다", a, b);
            else if (a<b)
                Console.WriteLine("{0}보다 {1}가 크다", b, a);
            else
                Console.WriteLine("{0},{1}는 같다.", a, b);
        }
        compare(11, 22);
    }
}

Result : 
11보다 22가 크다
```



## **References**

1. https://mrw0119.tistory.com/22
