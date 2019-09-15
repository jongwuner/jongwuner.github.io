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

**둘다 대리자(Delegate) 를 호출한다는 개념**

## **부연설명**

멀티스레드 환경에서 데이터 보호를 위해 beginInvoke를 써야 합니다.



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



모든 프로그램은 기본적으로 하나의 쓰레드로 시작이 된다. 따라서 폼을 화면에 그리는 메시지와 이벤트들도 그 쓰레드 안에서 구동이 된다. 하지만 사용자가 시작한 쓰레드는 이 쓰레드와는 별개로 실행이 된다. 따라서 이 커스텀 쓰레드에서 UI에 직접 접근을 하면 적절한 마샬링 없이 다른 쓰레드를 침범하는 것이다 (Cross Thread). 다시 말해, UI 쓰레드가 열심히 화면에 폼을 그리고 있는데 갑자기 다른 쓰레드가 와서 딴 짓을 하고 가는 꼴이 되버리는 것이다.

출처 - 

https://kworks.tistory.com/119

![1568538047344](C:\Users\jklh0\AppData\Roaming\Typora\typora-user-images\1568538047344.png)

worker Thread가 열심히 HookingInfo를 잡고 있다가, Output을 호출해서 왔는데, 

InvokeRequired. -> 여기는 UI의 영역인데 worker thread가 왔네? BeginInvoke를 통해 위임한다!

그 BeginInvoke를 통해 위임된 Output대리자는 textOutput.AppendText(strOutput)을 정상실행한다.



## **Invoke 예시**

```C#
/*
The following example demonstrates the 'Invoke(Delegate)' method of 'Control class.
A 'ListBox' and a 'Button' control are added to a form, containing a delegate
which encapsulates a method that adds items to the listbox.This function is executed
on the thread that owns the underlying handle of the form. When user clicks on button
the above delegate is executed using 'Invoke' method.


*/

using System;
using System.Drawing;
using System.Windows.Forms;
using System.Threading;

   public class MyFormControl : Form
   {
      public delegate void AddListItem();
      public AddListItem myDelegate;
      private Button myButton;
      private Thread myThread;
      private ListBox myListBox;
      public MyFormControl()
      {
         myButton = new Button();
         myListBox = new ListBox();
         myButton.Location = new Point(72, 160);
         myButton.Size = new Size(152, 32);
         myButton.TabIndex = 1;
         myButton.Text = "Add items in list box";
         myButton.Click += new EventHandler(Button_Click);
         myListBox.Location = new Point(48, 32);
         myListBox.Name = "myListBox";
         myListBox.Size = new Size(200, 95);
         myListBox.TabIndex = 2;
         ClientSize = new Size(292, 273);
         Controls.AddRange(new Control[] {myListBox,myButton});
         Text = " 'Control_Invoke' example";
         myDelegate = new AddListItem(AddListItemMethod);
      }
      static void Main()
      {
         MyFormControl myForm = new MyFormControl();
         myForm.ShowDialog();
      }
      public void AddListItemMethod()
      {
         String myItem;
         for(int i=1;i<6;i++)
         {
            myItem = "MyListItem" + i.ToString();
            myListBox.Items.Add(myItem);
            myListBox.Update();
            Thread.Sleep(300);
         }
      }
      private void Button_Click(object sender, EventArgs e)
      {
         myThread = new Thread(new ThreadStart(ThreadFunction));
         myThread.Start();
      }
      private void ThreadFunction()
      {
         MyThreadClass myThreadClassObject  = new MyThreadClass(this);
         myThreadClassObject.Run();
      }
   }

// The following code assumes a 'ListBox' and a 'Button' control are added to a form, 
// containing a delegate which encapsulates a method that adds items to the listbox.

   public class MyThreadClass
   {
      MyFormControl myFormControl1;
      public MyThreadClass(MyFormControl myForm)
      {
         myFormControl1 = myForm;
      }

      public void Run()
      {
         // Execute the specified delegate on the thread that owns
         // 'myFormControl1' control's underlying window handle.
         myFormControl1.Invoke(myFormControl1.myDelegate);
      }
   }
```





## **BeginInvoke 예시**

```C#
public delegate void InvokeDelegate();

private void Invoke_Click(object sender, EventArgs e)
{
   myTextBox.BeginInvoke(new InvokeDelegate(InvokeMethod));
}
public void InvokeMethod()
{
   myTextBox.Text = "Executed the given delegate";
}
```





## 마샬링





## References 

1. https://hjjungdev.tistory.com/94 
2. https://cartiertk.tistory.com/67
3. 다른 Thread를 통해 UI접근 1편 : https://ddochea.tistory.com/11?category=568955
4. 다른 Thread를 통해 UI접근 2편 : https://ddochea.tistory.com/12?category=568955

4. BeginInvoke vs Invoke 부연설명 : http://www.masque.kr/free/383086

5. BeginInvoke 부연설명 2 : https://docs.microsoft.com/ko-kr/dotnet/api/system.windows.forms.control.begininvoke?view=netframework-4.8

6. Invoke 부연설명 : https://docs.microsoft.com/ko-kr/dotnet/api/system.windows.forms.control.invoke?view=netframework-4.8

7. beginInvoke, Invoke이용해서 Thread ID 구하기 : https://freeprog.tistory.com/105?category=615404