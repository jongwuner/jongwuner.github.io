---


layout: post
comments: true
categories: C#
---

## **C# 서비스애플리케이션 프로젝트 만드는 법**

 윈도우즈 서비스 프로그램은 보통 Windows OS가 구동되면서 시스템에 의해 백그라운에서 자동으로 실행되는 프로그램이다. Windows Service 프로그램은 일반 콘솔이나 UI 프로그램과 달리, Session 0라고 불리우는 백그운드에서 실행되어 사용자가 UI 출력을 볼 수 없다. 따라서, 일반적으로 Event Log에 로그를 남기거나 파일과 같은 외부 저장 장치에 결과를 남기곤 한다.

![Service Project Template](http://www.csharpstudy.com/Practical/Image/Service-project.png)

Service1.cs 에서 Service1 클래스가 ServiceBase 클래스로부터 상속됨을 알 수 있다. Service1 클래스의 OnStart() 메서드는 서비스가 시작될 때 실행되며, OnStop() 메서드는 서비스가 멈출 때 실행된다. 



### 예제

```C#
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Diagnostics;
using System.Linq;
using System.ServiceProcess;
using System.Text;
using System.Threading.Tasks;
using System.Timers;
using System.Configuration;
using System.IO;
using System.Net;


namespace WindowsService1
{
    public partial class Service1 : ServiceBase
    {
        private Timer timer;
        private string dataFolder;

        public Service1()
        {
            InitializeComponent();
        }

        protected override void OnStart(string[] args)
        {
            dataFolder = ConfigurationManager.AppSettings["DataFolder"];

            timer = new Timer();
            timer.Interval = 5 * 60 * 1000; // 5분마다 실행
            timer.Elapsed += Timer_Elapsed; // Event가 발생하다. 
            timer.Start();
        }
		//*elapse : 경과하다.
        private void Timer_Elapsed(object sender, ElapsedEventArgs e)
        {
            string outputFile = Path.Combine(dataFolder, "csharp-news.html");

            WebClient cli = new WebClient();
            cli.DownloadFile("http://csharp.news", outputFile);
        }

        protected override void OnStop()
        {
        }
    }
}

```



![Windows Service Add Installer](http://www.csharpstudy.com/Practical/Image/Service-add-installer.png)



![Windows Service App 2](C:\Users\jklh0\source\github\img\Windows Service App 2.PNG)





![windows Service App](C:\Users\jklh0\source\github\img\windows Service App.PNG)



![Windows Service App 4](C:\Users\jklh0\source\github\img\Windows Service App 4.PNG)



![window service app 3](C:\Users\jklh0\source\github\img\window service app 3.PNG)

설치된 서비스를 삭제하기 위해서는 ``InstallUtil.exe /u MyService.exe ``명령을 수행하면 된다.



## 권한 오류



![windows Service App 5](C:\Users\jklh0\source\github\img\windows Service App 5.PNG)





## References

1. CSharpStudy : http://www.csharpstudy.com/Practical/Prac-service-program.aspx

2. Error 5 : Access is Denied : https://stackoverflow.com/questions/4267051/error-5-access-denied-when-starting-windows-service
3. How to add NETWORK SERVICE : https://serverfault.com/questions/469944/how-to-add-network-service-to-users-permission-group/469961