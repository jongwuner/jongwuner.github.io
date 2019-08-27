---
layout: post
comments: true
categories: ReactJS
---

## App.js

> Table로 Customer 정보 묶기

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
})

const customers = [{
  'id' : 1,
  'image' : 'https://placeimg.com/64/64/1',
  'name' : '이종추',
  'birthday' : '940217',
  'gender' : '남자',
  'job' : '군인'
},
{
  'id' : 2,
  'image' : 'https://placeimg.com/64/64/2',
  'name' : '이정환',
  'birthday' : '97년생',
  'gender' : '남자',
  'job' : '군인'
},
{
  'id' : 3,
  'image' : 'https://placeimg.com/64/64/3',
  'name' : '하정구',
  'birthday' : '96년생',
  'gender' : '남자',
  'job' : '군인'
},
{
  'id' : 4,
  'image' : 'https://placeimg.com/64/64/4',
  'name' : '신다민',
  'birthday' : '96년생',
  'gender' : '남자',
  'job' : '군인'
}
]

class App extends Component{
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
              {customers.map(c => {
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
            })}
          </TableBody>
        </Table>
      </Paper>
      )
    }
  }


export default withStyles(styles)(App);

```



* withStyles(styles)(App)
* paper
* class



## References****

1. **Material-ui** : https://material-ui.com/demos/tables/
2. 동빈나 Youtube : https://www.youtube.com/watch?v=YO9CqrnxbFU&list=PLRx0vPvlEmdD1pSqKZiTihy5rplxecNpz&index=6