---
layout: post
comments: true
categories: DB
---

# MySql 8.0.11 설치방법

<br><br><br>

## **SELECT 문 : 검색**

#### *SELECT [컬럼명] FROM [테이블명];*

- 해당 [테이블]의 해당[컬럼] 데이터를 불러옵니다. 컬럼 전체를 불러올 때는 컬럼명에 *를 넣으면 된다. <br>

  <br><br>

  <br>

#### *SELECT [컬럼명] FROM [테이블명] [WHERE 컬럼명 = 값];*

- WHERE 구문을 추가하여 해당 조건이 **참**인 데이터를 불러온다. <br> 

<br><br><br>

## **INSERT 문 : 삽입**

#### *INSERT INTO [테이블명] (컬럼명1, 컬럼명2, 컬럼명3, ...) VALUES (값1, 값2, 값3, ...);*

- 테이블명에 있는 컬럼명에 맞게 값을 입력합니다. 컬럼명과 값의 갯수는 동일합니다. 
- **※ 순서는 달라도 상관없습니다.**<br>

<br><br><br>

## **UPDATE 문 : 변경**

#### *UPDATE [테이블명] SET [컬럼명 = 변경할 값];*

- 테이블에 ㅔ있는 모든 데이터의 컬럼의 값을 변경합니다.<br>

<br>

<br><br>

#### *UPDATE [테이블명] SET [컬럼명 = 변경할 값] WHERE [컬럼명=값];*

- WHERE 절에 맞는 데이터만 변경합니다.<br>

<br><br><br>

#### *UPDATE [테이블명] SET [컬럼명1=변경할 값1, 컬럼명2=변경할 값2] WHERE [컬럼명=값];*

- 변경해야 할 컬럼이 여러 개일 때, 콤마를 사용한다.<br><br><br><br>

## **DELETE 문 : 삭제**

#### *DELETE from [테이블명];*

-  테이블에 있는 모든 데이터를 삭제한다.<br>

<br>

<br>

<br>

#### *DELETE from [테이블명] WHERE [컬럼명=값];*

- WHERE절에 맞는 데이터만 삭제합니다.<br>

<br>

<br><br>