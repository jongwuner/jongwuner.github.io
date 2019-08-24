---
layout: post
comments: true
categories: C#
---

[TOC]

Winform 프로그래밍을 하면서 쓰레드의 개념이 상당히 중요해진다. 쓰레드는 프로세스 안에서 여러가지 기능을 수행하는 단위이다. 해당 용어들을 이해하기 위해서는 쓰레드에 대한 개념이해가 선행이 되어야한다.<br>

기본적으로 C# Form 프로그래밍에서는 

- **MainThread**(UI Thread) 
- **OtherThread**( Work Thread)

로 분리되어 작업이 된다.

폼컨트롤 제어와 작업을 분리되어 하지 않고 MainThread가 모든 작업을 맡아 한다면 MainThread가 작업을 처리하는동안 사용자가 보고있는 Form이 반응 안하는 것처럼 느껴지고 실제로도 멈춰있게 된다. 그래서 분리해서 작업을 하게 된다.

그럼 위 3가지의 개념을 이해하기 위해 임의의 두 Thread가 있다고 가정하자.

하나의 예시를 들어보자 OtherThread에서 임의 작업 A를 마치고 버튼의 색을 빨간색으로 변경하고 싶다고 해보자 불가능하다.

왜냐하면 컨트롤을 생성한 MainThread에서만 접근이 가능하다 위 작업을 하려고하면 CrossThread Exception이 발생한다.

이 때 필요한 것이 **Invoke**, **BeginInvoke**이다.

그리고 이게 MainThread인지 OtherThread인지 구별해주는 **InvokeRequired**이 있는것이다.

Invoke가 필요한 Thread(OtherThread)라면 True MainThread(UI Thread)라면 False를 반환한다.



## **부연설명**

멀티스레드 환경에서 데이터 보호를 위해 Invoke를 써야 합니다.



응용 프로그램이 실행될 때 기본적으로 하나의 스레드가 발생합니다. 

이것을 Main 스레드라고 부르는 이유는 Main() 함수가 이 스레드의 시작점이기 때문입니다.

Main() 함수를 보시면 폼을 띄우죠? 결국 메인 스레드가 메인폼의 이벤트 처리를 담당하면서 

메인폼의 각종 컨트롤들의 값을 읽고 쓰는 작업을 수행합니다.



메인폼에서 다른 폼을 띄울 경우에도 기본적으로 메인 스레드가 자식 폼의 컨트롤들까지 모두 소유합니다. 

그런데, 별도의 스레드에서 폼의 컨트롤을 액세스하면 데이터(컨트롤?)가 깨질 수 있습니다. 

멀티스레드에 관해 조금이나마 공부해 보셨다면 이해하실 겁니다.



따라서, 별도의 스레드는 메인 스레드에게 컨트롤을 읽고 쓰는 작업을 위임하여 수행하게 하면 안전하겠죠.

그래서, 외부 스레드가 메인폼의 Invoke 를 호출하는 것입니다. 

**[별도의 스레드]에서 [main_form.Invoke(xxx) 를 호출]** 한다는 것은, 

**[별도의 스레드]가 [main_form 을 소유한 스레드]에게 [xxx 함수의 호출을 위임]한다는 뜻** 입니다.





https://cartiertk.tistory.com/67

## 마샬링





## References 

1. https://hjjungdev.tistory.com/94 
2. 다른 Thread를 통해 UI접근 1편 : https://ddochea.tistory.com/11?category=568955
3. 다른 Thread를 통해 UI접근 2편 : https://ddochea.tistory.com/12?category=568955