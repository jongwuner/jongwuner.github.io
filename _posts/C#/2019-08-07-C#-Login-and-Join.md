---
layout: post
comments: true
categories: C#
---

우선적으로 Mysql(workbench)을 통해 스키마를 생성한 후,   

name, age를 column으로 가지고 있는 table을 하나 생성한다.  

참고 : [[MySql]Workbench-설치-및-사용법](https://jongwuner.github.io/2019/08/07/MySql-Workbench-%EC%84%A4%EC%B9%98-%EB%B0%8F-%EC%82%AC%EC%9A%A9%EB%B2%95/)  

​        

그 이후, C#의 **Winform**을 간략하게 제작하여,   

**MySql**과 연동해본다.         



![photo1](https://user-images.githubusercontent.com/16419202/62713640-08cb8000-ba38-11e9-82f6-0342edd2f5cf.PNG)

#### 'MySqlConnect'라는 이름의 Winform 프로젝트를  생성한다.            

​          

​          



![photo2](https://user-images.githubusercontent.com/16419202/62713641-09641680-ba38-11e9-8555-f392b104268c.PNG)

#### ''아이디, 비밀번호' label을 한개씩 만들고, '로그인' 버튼을 생성한다.                    

 

  

-----------------------------------------

*MetroFrameWork  

*using Dapper  

---------------------

*Ref. 1*  : 윈폼 기본동작 강좌 (https://udpark.tistory.com/49)  

*Ref. 2* :  로그인폼과 DB Connect (https://marine1188.tistory.com/77)   