# React 项目内规范

## 目录
  - 结构
    - [文件结构](#文件结构)
    - [路由结构](#路由结构)
  - 书写规范
    - [Component](#component)
    - [Container](#container)
    - [Reducer](#reducer)
    - [公共组件](#公共组件)

---

### 文件结构

* 正常情况下，页面(片段)、container、component、reducer、action都是一一对应的，comopnent 则可以包含多个 components。

  当然，复杂则可以拆成多组(个)并由一个 component(container) 组合起来输出

  ```bash
    action
      page1.js          -> page1 的 action creators
      ...
    components
      page1.js          -> 通过 container 传递的 Props 显示页面(片段)并绑定事件
      page1.child1.js   -> page1 的一部分，当然如果简短可以直接写在 page1 里
      page1.child2.js   
      ...
    containers
      page1.js          -> 将状态及事件传递给 page1，并可以在此为 page1 绑上生命周期
      ...
    reducers
      page1.js          -> 根据 action 传入的 type 以及需要更新的 state 来更新 Store
      ...
  ```

### 路由结构
* 路由的首个Route为一个容器组件

  ```js
    // root component
    const Root = ({ children }) => (<div>{ children }</div>)
    // routes
    ...
    <Router history={ browserHistory } >
      <Route path='/[service]' component={ Root } >
        <IndexRoute component={ FirstPage } />
        ...
      </Route>
    </Router>
    ...
  ```
* path 命名小写多个单词以 “-” 分割，尽可能用名词
  ```js
    ...
    <Route path='food-list' component={ FoodList } />
    ...
  ```

### Component

* pure render，即：对于相同的props，总能给出相同的JSX输出（只做判断，不做修改）

* 尽量写函数式组件

  ```js
    const App = () => (<div></div>)
  ```

* 不要申明 JSX 的变量

  ```js
    // 不要这样做
    ...
      const XXX = (<div>xxx</div>)
      return (
        <div>{ XXX }</div>
      )
    ...
    // 推荐将其拆成组件
    ...
      const App = () => (<div><XXX /><div>)

      const XXX = () => (<div>xxx</div>)
    ...
  ```

* 不要在函数式组件里写复杂的逻辑代码，而将其封装成方法写在container里

* JSX用 “()” 包裹

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

### Container

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

### Reducer

* 尽量添加initialState

  ```js
      //即使它为空
      const initialState = {}
      const reducer1 = (state = initialState, action) => { ... }
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
