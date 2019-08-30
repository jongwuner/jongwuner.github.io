---
layout: post
comments: true
categories: ReactJS
---

## **Material-ui에서 가져오기**



![1567080100955](C:\Users\jklh0\AppData\Roaming\Typora\typora-user-images\1567080100955.png)



![1567080048845](C:\Users\jklh0\AppData\Roaming\Typora\typora-user-images\1567080048845.png)



### 소스코드

```javascript
import React from 'react';
import { makeStyles } from '@material-ui/core/styles';
import CircularProgress from '@material-ui/core/CircularProgress';

const useStyles = makeStyles(theme => ({
  progress: {
    margin: theme.spacing(2),
  },
}));

export default function CircularIndeterminate() {
  const classes = useStyles();

  return (
    <div>
      <CircularProgress className={classes.progress} />
      <CircularProgress className={classes.progress} color="secondary" />
    </div>
  );
}
```







## References****

1. **Material-ui** : https://material-ui.com/demos/tables/
2. 동빈나 Youtube : https://www.youtube.com/watch?v=YO9CqrnxbFU&list=PLRx0vPvlEmdD1pSqKZiTihy5rplxecNpz&index=6