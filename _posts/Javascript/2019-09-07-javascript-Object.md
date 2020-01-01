---
layout: post
comments: true
categories: Javascript
---



## **객체(Object)를 생성하는 방법**

```javascript
var grades = {'egoing' : 10, 'k8805' : 6, 'sorialgi': 80};
```



> \> grades
>
> \> Object {egoing: 10, k8805: 6, sorialgi: 80}



```javascript
var grades = {};
grades['egoing'] = 10;
grades['k8805'] = 6;
grades['sorialgi'] = 80
```



```javascript
var grades = new Object;
grades['egoing'] = 10;
grades['k8805'] = 6;
grades['sorialgi'] = 80
```

> \> grades['egoing']
>
> \> 10
>
> \> grades['k8805']
>
> \> 6



## **반복문과 객체**

```javascript
var grades = {'egoing' : 10, 'k8805' : 6, 'sorialgi': 80};
for(key in grades){
    document.write("key : "+key+" value : "+grades[key]+ "<br/>" );
}+
```





## **객체에 함수를 담을수도 있다.**

```javascript
var grades = {
	'list' : {'egoing' : 10, 'k8805' : 8, 'sorialgi' : 80} 
	'show' : function(){
        alert('Hello world');
    }
}
alert(grades['list']['egoing']);
alert(grades['show']())

result : 
10
Hello world

```

> 객체 안에 함수를 저장할 수도 있다. 이런 식으로 저장이 가능하다. 





## **객체지향 프로그래밍**

```javascript
var grades = {
	'list' : {'egoing':10, 'k8805':8, 'sorialgi':80},
    'show' : function(){
        for(var name in this.list){
        console.log(name, this.list[name]);
        }
    }
}
grades['show']();

```

