---
layout: post
comments: true
categories: Javascript
---



## **다양한 정의방법**

```javascript
var member = ['egoing', 'k8805', 'sorialgi'];
alert(member[0]);
alert(member[1]);
alert(member[2]);
```



## **함수! 배열형 반환이 가능**

```javascript
function get_members(){
	return ['abcd', 'efgh', 'qwer'];
}

var = members = get_members();
document.write(members[0]);
document.write(members[1]);
document.write(members[2]);
```



## **push, pop**

```javascript
var li = ['a', 'b', 'c', 'd'];
li.push('f');
alert(li);

result : ["a", "b", "c", "d", "f"];
```



## **제거, 정렬**

