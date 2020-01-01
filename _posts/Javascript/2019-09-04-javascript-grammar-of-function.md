---
layout: post
comments: true
categories: Javascript
---

정의와 호출을 `<script>``</script>`내부에서 가능하다!

```javascript
...
<script>    
    function numbering(){
        i = 0;
        while(i < 10){
            document.write(i);
            i += 1;
        }
    }
    numbering();
	numbering();
</script>
...
```



## **다양한 정의방법**

> 기본적인 함수 정의

```javascript
function a(){
	return 'abcd';
}
...
a()
```



> 변수에 함수 넣기

```javascript
numbering = function(arg){
	retrun arg;
}
```



> 익명함수

```javascript
(function(arg){
	return arg;
})()
```

