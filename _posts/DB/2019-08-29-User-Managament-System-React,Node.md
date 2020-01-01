---
layout: post
comments: true
categories: DB
---

[TOC]



## **HeidiSQL**

![1567084341740](C:\Users\jklh0\AppData\Roaming\Typora\typora-user-images\1567084341740.png)



 ### SQL문**

```mysql
USE management;

CREATE TABLE CUSTOMER(
	id INT PRIMARY KEY AUTO_INCREMENT,
	image VARCHAR(1024),
	NAME VARCHAR(64),
	birthday VARCHAR(64),
	gender VARCHAR(64),
	job VARCHAR(64)
) DEFAULT CHARACTER SET UTF8 COLLATE UTF8_GENERAL_ci;
```





![1567084945647](C:\Users\jklh0\AppData\Roaming\Typora\typora-user-images\1567084945647.png)



![1567084960183](C:\Users\jklh0\AppData\Roaming\Typora\typora-user-images\1567084960183.png)



## **React.js, Node.js 와 연동**





![1567085485278](C:\Users\jklh0\AppData\Roaming\Typora\typora-user-images\1567085485278.png)



```javascript
const fs = require('fs');
```



```javascript
app.get('/api/customers', (req, res) => {
  res.send();
})
```



```javascript
const data = fs.readFilelSync('./database.json');
const conf = JSON.parse(data);
const mysql = require('mysql');

const connection = mysql.createConnection({
  host: conf.host,
  user: conf.user,
  password: conf.password,
  port: conf.port,
  database: conf.database
});

connection.connect();
```



```javascript
app.get('/api/customers', (req, res) => {
//  res.send();
    connection.query(
      "SELECT * FROM CUSTOMER",
      (err, rows, fields) => {
        res.send(rows);
      }
    )
})
```

