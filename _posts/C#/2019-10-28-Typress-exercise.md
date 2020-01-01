---
layout: post
title: "Typress exercise"
subtitle: 'Typress ''로그인->마일리지'' 종료이벤트 예제'
author: "jjongwuner"
header-style: text
tags:
  - C#
  - Projects
---

## 

## Ex

```C#
using System;
using System.Threading;

namespace aa
{
    public delegate void MyDelegate(AutoResetEvent ev);

    public class Example
    {

        public static AutoResetEvent MainEv = new AutoResetEvent(false);

        public static void AddPrintJob(AutoResetEvent ev)
        {
            Console.WriteLine("프린터 인쇄가 요청되었습니다.");
            ev.Set();
            Thread.Sleep(3000);
        }

        static void Main(string[] args)
        {
            Console.WriteLine("Typress Server 시작\n");

            MyPrinter p = new MyPrinter();
            p.PrintRequest += new MyDelegate(AddPrintJob);

            ThreadStart p1 = new ThreadStart(p.WaitPrintRequest);
            Console.WriteLine("Printer Service 시작");

            ThreadStart p2 = new ThreadStart(p.PushPrintRequest); // 외부 이벤트
            Thread p_1 = new Thread(p1);
            Thread p_2 = new Thread(p2);
            p_1.Start();
            p_2.Start();

            MainEv.WaitOne(); // p1이 종료되는 이벤트 !!

            MyPrinter.PushEv.Reset();
            MyPrinter.PushFlag = false;
            Console.WriteLine("Typress Server 종료\n");
        }
    }

    public class TaskInfo
    {
        public RegisteredWaitHandle Handle = null;
        public string OtherInfo = "default";
    }

    class MyPrinter
    {
        public event MyDelegate PrintRequest;
        public static AutoResetEvent PrintEv = new AutoResetEvent(false);
        public static ManualResetEvent PushEv = new ManualResetEvent(true);
        public static bool PushFlag = true;
        public AutoResetEvent ev = new AutoResetEvent(false);
        // Print 대기.
        // Print 들어왔음 -> 로그인 인증, 완료하면 다시 대기.  
        public void WaitPrintRequest()
        {
            TaskInfo ti = new TaskInfo();
            ti.OtherInfo = "Printer Open";

            Console.WriteLine("WaitProc( {0} ) executes on thread {1}; cause = YET",
                ti.OtherInfo,
                Thread.CurrentThread.GetHashCode().ToString());
            ti.Handle = ThreadPool.RegisterWaitForSingleObject(ev, new WaitOrTimerCallback(WaitProc), ti, 1000, false);


            PrintEv.WaitOne();

            Console.WriteLine("Main Thread 진행");
            Thread.Sleep(1000);
            Example.MainEv.Set();
        }
        public void PushPrintRequest()
        {
            while (PushFlag && PushEv.WaitOne())
            {
                Console.ReadLine();
                PrintRequest(ev);
            }
            Console.WriteLine("Push 종료!");
        }

        public static void WaitProc(object state, bool timedOut)
        {
            // The state object must be cast to the correct type, because the
            // signature of the WaitOrTimerCallback delegate specifies type
            // Object.
            TaskInfo ti = (TaskInfo)state;

            ti.OtherInfo = "Printer Waiting";
            string cause = "No Printer Request";
            if (!timedOut)
            {
                cause = "Add Print Job!!";
                // If the callback method executes because the WaitHandle is
                // signaled, stop future execution of the callback method
                // by unregistering the WaitHandle.
                if (ti.Handle != null)
                {
                    Console.WriteLine("Typress Auth!");
                    ti.Handle.Unregister(null);
                    PrintEv.Set();
                }
            }

            Console.WriteLine("WaitProc( {0} ) executes on thread {1}; cause = {2}.",
                ti.OtherInfo,
                Thread.CurrentThread.GetHashCode().ToString(),
                cause
            );
        }
    }
}




```

----------

