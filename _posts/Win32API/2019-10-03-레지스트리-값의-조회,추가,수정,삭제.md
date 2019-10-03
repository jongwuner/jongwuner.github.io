---

layout: post
comments: true
categories: Win32API
---

## **Registry 키의 조회/생성/삭제**

![image](https://user-images.githubusercontent.com/16419202/66097614-0e79b800-e5da-11e9-87a6-c54dada3f47e.png)



##### ---RegQueryValue : 지정한 키의 기본값을 가져온다.

```C++
LONG WINAPI RegQueryValue(
	__in HKEY hKey,
    __in_opt LPCTSTR lpSubKey,
    __out_opt LPTSTR lpValue,
    __inout_opt PLONG lpcbValue
);
```

- **hKey :** 기본값을 가져올 키의 상위 키를 지정한다.

- **lpSubKey :** hKey의 서브키 중 기본 값을 가져올 키의 이름을 지정합니다.

  만일 NULL이거나 빈 문자열("")이면, hKey 자체의 기본 값을 가져옵니다.

- **lpValue :** 기본 값을 담아올 버퍼. 
- **lpcbValue** : lpValue 버퍼 크기를 일러주거나 가져옵니다. 단위는 바이트

**※ 반환을 성공할 경우에 ERROR_SUCCESS를 반환합니다.**



##### ---RegSetValue : 지정한 키의 기본값을 설정한다

```C++
LONG WINAPI RegSetValue(
	__in HKEY hKey,
    __in_opt LPCTSTR lpSubKey,
    __in DWORD dwType,
    __in LPCTSTR lpData,
    __in DWORD cbData
);
```

- hKey : 기본 값을 설정할 키의 상위키입니다.
- lpSubKey : hKey의 서브키중에서 기본 값을 설정할 키의 이름입니다.
- dwType : 설정할 값의 타입입니다. 반드시 REG_SZ만을 써야합니다.
- lpData : 설정할 문자열 데이터입니다.
- cbData : 문자열의 길이를 명시하지는 않고, 함수 내부에서 lpData 문자열의 길이를 계산한다.

**※ 반환을 성공할 경우에 ERROR_SUCCESS를 반환합니다.**<br><br>

> 첫번째

![image](https://user-images.githubusercontent.com/16419202/66098221-babc9e00-e5dc-11e9-92df-116194e30fb3.png)

> 두번째

![image](https://user-images.githubusercontent.com/16419202/66098287-f3f50e00-e5dc-11e9-9cab-2913d8261a01.png)

> 세번째

![image](https://user-images.githubusercontent.com/16419202/66098304-0a9b6500-e5dd-11e9-8be8-55b10ffd9da6.png)

## **References**

1. 윈도우 레지스트리 : https://ko.wikipedia.org/wiki/윈도우_레지스트리)
2. 기본값의 조회/수정 : https://tapito.tistory.com/11?category=397312