<!-- # React 项目内规范 -->


### 命名规范

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


### 方法 & 留白 & 判断

* 方法通过匿名函数来赋值创建

  ```js
    //function
    const create = function() {}
    //arrow function
    const create = () => {}

    create()
  ```

* 如果可以就不要加分号啦，注意换行就行

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

* 正常情况下请使用 “===”，“!==” 来比较是否相等

### components

* pure render，即：对于相同的props，总能给出相同的JSX输出（只做判断，不做修改）

* 尽量写函数式组件

  ```js
    const App = () => (<div></div>)
  ```
* 不要在函数式组件里写复杂的逻辑代码，
  而将其封装成方法写在container里当props传入component

* JSX用 “()” 包裹，如：(\<p>\</p>)

* 尽量不要在JSX内使用对象来进行赋值，而在 return 前将对象的参数提取出来（描述不清楚）

  ```js
    ...
    (<div>{ o.name }</div>)
    ...
    //预先提取
    ...
    const { name } = o
    (<div>{ name }</div>)
    ...
  ```

* 默认值尽量在reducer里定义好

### containers

* mapStateToProps参数内将需要用到的state从Store里提取出来

  ```js
    //如：Store = { state1: page1State, state2: page2State }
    const mapStateToProps = ({ state1, state2 }) => ({ ...state1, ...state2 })
  ```

* mapDispatchToProps内的方法都以 handle 开头

  ```js
    const mapDispatchToProps = dispatch => ({
      [ dispatch, ] //如果用到 wrap 方法的话需要添加
      handleChange: () => { ... },
      handleClick : () => { ... }
    })
  ```

### 公共组件

* 私有方法都以 handle 开头

* 对外公开的方法都以 on 开头，如：onClick、onChange、onSuccess（尽量通用，尽量语义）

  ```js
    //common component
    class Test extends Component {
      constructor(props) {
        super(props)
        this.state = { word: '' }
      }
      handleSuccess() {
        //从 props 里提取出 onSuccess
        const { onSuccess } = this.props
        const { word }      = this.state
        onSuccess(word)
      }
      handleChange(word) {
        this.setState({ word })
      }
      render() {
        return (
          <div>
            <input type='text'   onChange={ e => this.handleChange(e.target.value) } />
            <input type='button' onClick={ this.handleSuccess } />
          </div>
        )
      }
    }

    //
    ...
    <Test onSuccess={ word => console.log(word) } />
    ...

  ```
