# react+redux开发记录
------------------

### 开发技术栈
	react
	redux
	webpack
	antd-mobile
	es6
	sass

### 学习资源推荐
1. [Hello World --React](https://facebook.github.io/react/docs/hello-world.html)
2. [es6/es2015 核心内容](http://www.jianshu.com/p/ebfeb687eb70?utm_campaign=hugo&utm_medium=reader_share&utm_content=note&utm_source=qq)
3. [前端之 Sass/Scss 实战笔记](http://url.cn/45mI7ZJ)
4. [Redux 中文文档](http://cn.redux.js.org/index.html)
5. [ANT DESIGN MOBILE](https://mobile.ant.design/components/drawer/)
6. [Webpack的全面介绍，模块Bundler](http://www.theodo.fr/blog/2016/07/a-comprehensive-introduction-to-webpack-the-module-bundler/?utm_source=webpack_official_documentation)
7. [其他相关资源推荐](http://www.jianshu.com/p/a1790e1945a8?utm_campaign=hugo&utm_medium=reader_share&utm_content=note&utm_source=qq)

### 开发环境的搭建
   SourceTree添加远端仓库oto_saas_web_app_rebuild，新建一个develop分支。  
	相关终端操作：
	
	/* 根据package.json文件安装依赖 */
	$ npm i
	
	/* install命令之前，登陆npm账号，如果已登陆，请忽略 */
	$ npm login
	
	/* 生成shenghuojiaofei相关文件夹 */
	$ node creator.js shenghuojiaofei
	
	/* 本地开发，默认端口：localhost:9000 */
	$ npm run shenghuojiaofei
	/* 本地开发，自定义端口：localhost:20000 */
	$ npm run shenghuojiaofei 20000
	
	/* 生成静态资源，用于生产 */
	$ npm run shenghuojiaofei_build
    
### 目录结构

    |-- assets                                 // 存放html
    |-- config                                 // webpack配置
    |   |-- _                                  // 抽离出来的webpack配置文件
    |   |-- shenghuojiaofei                    //个人项目webpack配置（node create.js shenghuojiaofei自动生成）
    |-- dist                                   // build后静态资源
    |-- src                                    // 项目开发目录
    |   |-- services                           // 重构的所有项目
    |   |   |-- shenghuojiaofe                 // 单个项目(node create.js shenghuojiaofei自动生成）
    |   |   |   |-- actions                    // 存放redux中的action模块
    |   |   |   |   |-- index.js      	       // 例：首页action
    |   |   |   |-- components                 // 显示组件
    |   |   |   |   |-- index.js      	       // 例：首页显示组件
    |   |   |   |-- containers                 // 容器组件
    |   |   |   |   |-- index.js               // 例：首页容器组件
    |   |   |   |-- reducers                   // 存放redux中的reducers模块
    |   |   |   |   |-- index.js               // 例：页面的reducers树
    |   |   |   |   |-- myServices.js          // reducers树的myServices分枝
    |   |   |   |-- styles                     // 存放当前项目所用到的样式
    |   |   |   |   |-- index.scss             // 例：首页样式
    |   |   |   |-- index.js                   // 当前项目入口配置文件
    |   |   |   |-- img                        // 所有项目用到的图片文件scss文件
    |   |   |   |-- index.scss                     
    |-- .babelrc                               // babel文件配置
    |-- .gitignore                             // push忽略文件
    |-- package.json                           // 依赖及配置记录文件
    |-- README                                 // 简介
    |-- path.config.js                         // webpack的配置文件


### react必备技能参考
	了解基础的jsx语法，和样式写法，以及react的函数和es6类声明这两种组件的定义方法。
	
### redux自我小结（个人小结，仅供参考）
	参照redux官方文档，结合里面的demo去熟悉redux管理数据的思想。
     redux的出现，是为了解决react中组件过多时，组件状态之间会互相影响，导致数据不好控制，并且后期添加新需求时的复杂性也很大。  
     redux基于单向数据流的设计思想：所有的数据都被放倒一个store（状态树）中进行管理，只能通过action来发送改变store中的某个state的信号，最后通过自定义的纯函数reducer，来将新的state浅合并到store树中，store树感受到某个分枝上的的数据较之前的数据有更新后，就会更新这个state所在的组件，并将组件重新渲染到浏览器中。
>一个比较有意思的比喻：  
     把 js 比喻成巴士，把 store, container, reducer 比喻为三个车站，再把 state 
