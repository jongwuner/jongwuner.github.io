---
layout: post
comments: true
categories: Python
---





**map**은 **list**의 요소를 **지정된 함수**로 처리하는 함수이다. map은 원본 리스트를 변경하지 않고 새 리스트를 생성한다.<br><br><br>

> map을 사용하지 않은 예(대화형 Python)

```python
>>> a = [1.5, 3.5, 2.7]
>>> for i in range(len(a))
...		a[i] = int(a[i])
...
>>> a
[1, 3, 2]
```

이런 식으로 **C/C++** 처럼 반복문으로 요소마다 모두 접근을 해야 한다.<br>

하지만 map을 사용하면 간편하게 list의 모든요소에 간결하게 접근할 수 있다.<br><br>

 <br>

> map을 사용한 예

```Python
>>> a = [1.5, 3.5, 2.7]
>>> a = list(map(int, a))
>>> a
[1, 3, 2]
```

<br><br>

### **map의 범용성(자료형)**

map에는 리스트 뿐아니라 모든 `반복가능한 객체`를 넣을 수 있다. 

``` Python
>>> a = list(map(str, range(5)))
>>> a
['0', '1', '2', '3', '4']
```



## **Input().split()과 map**

`input().split()`으로 여러 개의 값을 입력받고 정수, 실수로 변환할 때도 map을 사용했었는데, `input().split()` 의 결과가 문자열 리스트여서 map을 사용할 수 있었다.<br>

<br>

> input().split()으로 10 20을 입력받은 경우

```Python
>>> a = input().split()
10 20
>>> a
['10', '20']
```

<br>

10 20을 입력하면 ``['10', '20']`` 처럼 문자열 2개가 들어가있는 리스트가 만들어진다.<br>

<br>

> input().split()으로 10 20을 입력받고 map을 통해 int로 변환

```Python
>>> a = map(int, input().split())
10 20
>>> a
<map object at 0x03DFB0D0>
>>> list(a)
[10, 20]
```

`list(a)`를 통해 list안에 들어가있는 int형 정수 2개를 뽑을 수 있었다.



-------------

Ref.  https://dojang.io/mod/page/view.php?id=2286