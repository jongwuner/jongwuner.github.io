---
layout: post
comments: true
categories: ReactJS
---

## Rest API란?

## JSON 처리법

- jsonlint

## Proxy란?



## State vs probs

state는 변경가능<br>

probs는 일정

### **예제**

```javascript
import React, {Component} from 'react';
import logo from './logo.svg';
import Customer from './components/Customer';
import './App.css';
import Paper from '@material-ui/core/Paper';
import Table from '@material-ui/core/Table';
import TableHead from '@material-ui/core/TableHead';
import TableBody from '@material-ui/core/TableBody';
import TableRow from '@material-ui/core/TableRow';
import TableCell from '@material-ui/core/TableCell';
import { withStyles } from '@material-ui/core/styles';

const styles = theme => ({
  root: {
    width : '100%',
    marginTop : theme.spacing.unit * 3,
    overflowX : "auto"
  },
  table: {
    minWidth: 1080
  }
});



class App extends Component{

  state = {
    customers: ""
  }

componentDidMount(){
  this.callApi()
    .then(res => this.setState({customers: res}))
    .catch(err => console.log(err))
}

callApi = async() => {
  const response = await fetch('/api/customers');
  const body = await response.json();
  return body;
}

  render(){
    const { classes } = this.props;
    return (
      <Paper className = {classes.root}>
        <Table className = {classes.table}>
          <TableHead>
            <TableCell>번호</TableCell>
            <TableCell>이미지</TableCell>
            <TableCell>이름</TableCell>
            <TableCell>생일</TableCell>
            <TableCell>성별</TableCell>
            <TableCell>직업</TableCell>
          </TableHead>
          <TableBody>
              {this.state.customers ? this.state.customers.map(c => {
                return(
                <Customer
                  id={c.id}
                  image={c.image}
                  name={c.name}
                  birthday={c.birthday}
                  gender={c.gender}
                  job={c.job}
                />
              );
            }) : ""}
          </TableBody>
        </Table>
      </Paper>
      )
    }
  }


export default withStyles(styles)(App);

```



```javascript
componentDidMount(){
  this.callApi()
    .then(res => this.setState({customers: res}))
    .catch(err => console.log(err))
}

```

```javascript
callApi = async() => {
  const response = await fetch('/api/customers');
  const body = await response.json();
  return body;
}
```

- 8강 13분21초

## References****

1. **Material-ui** : https://material-ui.com/demos/tables/
2. 동빈나 Youtube : https://www.youtube.com/watch?v=YO9CqrnxbFU&list=PLRx0vPvlEmdD1pSqKZiTihy5rplxecNpz&index=6