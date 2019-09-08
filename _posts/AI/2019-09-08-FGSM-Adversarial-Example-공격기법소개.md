---
layout: post
comments: true
categories: AI
---

## **GFSM: Adversarial Example**

적대적 예제를 통해 전혀 다른 결과를 낳게 되게끔 야기

![1567913252864](C:\Users\jklh0\AppData\Roaming\Typora\typora-user-images\1567913252864.png)



## Deep Neural Network(DNN)

![1567913235636](C:\Users\jklh0\AppData\Roaming\Typora\typora-user-images\1567913235636.png)

손상된 표지판도 올바르게 인식할 수 있음.



![1567913380615](C:\Users\jklh0\AppData\Roaming\Typora\typora-user-images\1567913380615.png)



x -> Input Latyer에 들어갈 때 : 64 x 64 x 3 의 크기를 일렬로 나열한 배열에다가 삽입함.

Hidden Layer : 해당 이미지에 대한 Feature을 추출한다.

Output Layer : 사용자가 얻고자 하는 데이터를 얻을 수 있음.

어느정도의 확률로 Panda라고 판단하는지 확률을 다루게 됨



### Cost Function(경사 하강법)

![1567913661607](C:\Users\jklh0\AppData\Roaming\Typora\typora-user-images\1567913661607.png)

- y 로 드는 비용 x
- 입력으로 들어오는 x



### Problem Description

![1567913990998](C:\Users\jklh0\AppData\Roaming\Typora\typora-user-images\1567913990998.png)

인간에게는 큰 변형이 안일어났지만, 컴퓨터의 입장에서는 큰 변화!



![1567914172292](C:\Users\jklh0\AppData\Roaming\Typora\typora-user-images\1567914172292.png)



![1567914435505](C:\Users\jklh0\AppData\Roaming\Typora\typora-user-images\1567914435505.png)



## References

- https://www.youtube.com/watch?v=TfDO2guk0ug