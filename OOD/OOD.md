

## 如何评判一轮OOD面试

### Single Responsibility Principle

一个类应该有且只有一个去改变他的理由， 这意味着一个类应该只有一项工作

![Screen Shot 2019-06-01 at 9.25.26 PM](/Users/zoey_oo.oo/Desktop/Notes/OOD/img/Screen Shot 2019-06-01 at 9.25.26 PM.png)

使代码更加clean， 责任更加clean，

### open close principle 开放封闭原则

open to extension, close to modification 

对象或实体应该对扩展开放， 对修改封闭

需要扩展性很好

可以减少代码量，

一个class 能extend 一个parent class， 能implements 很多个interface 

### Liskov substitution principle 里氏替换原则

任何一个子类 或者派生类应该可以替换他们的基类或父类

父类： human

子类： Asian，American

新的类： robot （robot不应该继承human这个父类）所以违背了这个原则

不能设计一个不合适的继承

### Interface segration principle 

不应该强迫一个类实现它用不上的接口

![Screen Shot 2019-06-01 at 9.46.00 PM](/Users/zoey_oo.oo/Desktop/Notes/OOD/img/Screen Shot 2019-06-01 at 9.46.00 PM.png)

Cube是立体的， Rectangle是平面的， 当Rectangle继承了Shape，我们强迫了Rectangle继承了它用不到的calculateArea



### Dependency Inversion Principle

抽象不应该依赖于具体实现， 具体实现应该依赖于抽象，High-Level的实体不应该依赖于low-level的实体

在类A里定义了一个object B， 还有一个类叫B，

A是depend on B

当我们的B有任何的改变的时候，比如说改名字叫B+，我们的A没法正常的work了

当我们要去设计一个high level（涉及到不同层次）比如说area calculator，我们尽量把接口依赖于一些抽象比如说shape

用微信

## 面试中应该怎么做

### 实战演练

 can you design an elevator system for a building 

5C 解题法

Clarify 

- what 
  - 抓关键字，找名词
    - Glass of water： what kind of glass， what kind of water
    - Elevator for building：
      - elevator 的属性： 
        - 承重量/多少人 （common sense）x 尴尬问题
        - 有没有重量的限制，
        - type： 客梯，货梯 =》有没有不同的种类，他们有什么区别，
      - building：
        - 多高，多少人 x 尴尬问题，对解题没有帮助
        - 是否有多处能搭乘的电梯口， 当收到一个搭乘的请求时候， 有多少台电梯能够响应
- how （也不一定要问完全部问题，一定要有clarify的步骤）
  - 怎么判断电梯是否超重
  - 当按下按钮时， 哪一台电梯会响应， 
    - 同方向》静止〉反方向
    - 一半负责奇数，一半负责偶数
  - 但电梯在运行时，哪些按键可以响应

Core objects

- 
- 

