---
layout: post
comments: true
categories: Win32API
---

## **Registry 키의 조회/생성/삭제**

<br>

##### ---RegEnumKey : 지정한 키의 서브키들을 조회한다.

 ```C++
LONG WINAPI RegEnumKey(
	__in HKEY hKey,
	__in DWORD dwIndex,
	__out LPTSTR lpName,
	__in DWORD cchName
);
 ```

- **hKey :** 서브키를 조회할 대상 키입니다.
- **dwIndex :** 몇 번째 서브키의 이름을 가져올 것인지 지정합니다.
- **lpName :** 서브키의 이름을 담아 올 문자열 버퍼입니다.
- **cchName :** lpName 버퍼의 길이(단위 : 문자)입니다.

**※ 함수 수행 성공 시 ERROR_SUCCESS, 더이상의 서브키가 없다면 ERROR_NO_MORE_ITEMS를 반환한다.**<br>

<br><br>

##### --- RegCreateKey : 지정한 키의 서브키로 새 키를 만듭니다.

```C++
LONG WINAPI RegCreateKey(
	__in HKEY hKey,
	__in_opt LPCTSTR lpSubKey,
	__out PHKEY phkResult
);
```

- **hKey** : 서브키를 만들 대상 키입니다.
- **lpSubKey** : 새 서브키의 이름입니다.
- **phkResult** : 새로 만들어진 서브키에 대한 핸들을 얻어옵니다.

**※ 함수 수행 성공 시 ERROR_SUCCESS**<br><br>

> 사용법 : "HKLM\SoftWare\Tapito" 키를 만드려고 할 때,

```C++
HKEY hKey, hNewKey;

RegOpenKey(HKEY_LOCAL_MACHINE, TEXT("SoftWare"), &hKey);
RegCreateKey(hKey, TEXT("Tapito"), &hNewKey);
```



**--- RegDeleteKey : 지정한 키의 서브키를 지웁니다. 이 때, 지울 서브키 안에는 또 다른 서브키가 		없어야 합니다.**

```C++
LONG WINAPI RegDeleteKey(
	__in HKEY hKey,
	__in LPCTSTR lpSubKey
);
```

- hKey : 삭제할 키가 있는 상위 키입니다.
- lpSubKey : 삭제할 키의 이름입니다.

**※ 함수 수행이 성공하면 ERROR_SUCCESS를 반환합니다.**



> 1번

![image](https://user-images.githubusercontent.com/16419202/66096334-9e693300-e5d5-11e9-8930-da2048bea71a.png)



> 2번
>
> ![image](https://user-images.githubusercontent.com/16419202/66096527-39faa380-e5d6-11e9-9857-e30ac4f4540d.png)



> 3번
>
> ![image](https://user-images.githubusercontent.com/16419202/66096574-61517080-e5d6-11e9-8e1a-4ae0f8ea4946.png)

## References**

1. http://blog.naver.com/PostView.nhn?blogId=fablezzg&logNo=10031033283&redirect=Dlog&widgetTypeCall=true

2. 레지스트리 읽기 / 쓰기 : http://zbaekhk.blogspot.com/2011/06/mfc_16.html

3. 레지스트리 서브트리 구성별 : https://m.blog.naver.com/PostView.nhn?blogId=rbdi3222&logNo=220597850076&proxyReferer=https%3A%2F%2Fwww.google.com%2F
4. 레지스트리 위키 : [https://ko.wikipedia.org/wiki/%EC%9C%88%EB%8F%84%EC%9A%B0_%EB%A0%88%EC%A7%80%EC%8A%A4%ED%8A%B8%EB%A6%AC](https://ko.wikipedia.org/wiki/윈도우_레지스트리)