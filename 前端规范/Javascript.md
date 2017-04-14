# Javascript 规范

### 目录
  - 语法
    - [建议](#建议)
    - [命名](#命名)
    - [注释](#注释)
    - [留白](#留白)
  - 方法
    - [函数](#函数)
    - [逻辑运算](#逻辑运算)

---

### 建议

* 如果可以就不要加分号啦，注意换行就行

### 命名

* 文件夹名，小写，多个单词以 “-” 分割（服务不分割），如：order-list、jiadianqingxi、cashier

* 文件名，小写，多个单词以 “-” 分割，如：index.scss、app.js

* 类名，大驼峰命名，

  ```js
    class App extends Component { ... }
    //函数式
    const App = () => (<div></div>)
  ```

* 方法名，小驼峰命名，如：

  ```js
    const createOrder = () => {}
    const mergeState = () => {}
  ```

* 参数 / 变量，小驼峰命名

  ```js
    let customerCode
    let customerUserId
  ```

* 常量，大写，多个单词以 “\_” 分割

  ```js
    const REQUEST_URL   = 'http://...'
    const TIME_INTERVAL = 1000
  ```


### 注释

* 专有名词或冷门单词请注释

  ```js
    //我是不是有一只香蕉
    let woshibushiyouyizhixiangjiao = false
  ```
* 方法请注释，复杂或多参的情况请使用多行注释标明参数（可以了解一下 [类型签名](https://github.com/llh911001/mostly-adequate-guide-chinese/blob/master/ch7.md)）

### 留白

* 缩进大小 = 4个空格（编辑器可以设置）

* “,”，“:” 之后跟空格

  ```js
    const a = {
      b: 1,
      c: [ 1, 2, 3 ]
    }
  ```

* “{}”，“[]” 开始和结束都加空格

  ```js
    const arr = [ 1, 2, 3 ]
    const obj = { p: 1, p: 2 }
  ```
* 三目运算按操作符换行并注意缩进（当较长的时候）

  ```js
    //三目
    typeof o === 'undefined'
      ? false
      : typeof o === 'array'
        ? false
        : typeof o === 'object'
          ? true
          : false
  ```

* 运算符前后加空格（++，\-\- 除外）

  ```js
    let a = 1
    let b = a + 2
  ```

### 函数

* 函数通过赋值变量来创建

  ```js
    //function
    const create = function() {}
    //arrow function
    const create = () => {}

    create()
  ```

### 逻辑运算

* 正常情况下请使用 “===”，“!==” 来比较是否相等
