## 前端工程化

### 1、Git与工作流
  #### Git功能场景实战
  #### 工作流
    Git flow
  #### Eslint与代码规范
    Eslint Prettier
  #### CI持续集成
    CI/CD 持续集成/部署
### 2、前端构建实战
  #### webpack基础与性能优化
    `Webpack配置: https://webpack.docschina.org/configuration/`
    `sourcemap`
    `libraryTarget`
    `CommonJS规范`
  #### Lerna 在项目中应用
    `Lerna 是一个管理工具，用于管理包含多个软件包（package）的 JavaScript 项目。`
    `默认lerna有两种管理模式，固定模式和独立模式`
  #### 模块规范
  #### TreeShaking
  #### Webpack 插件开发实战
  #### Babel 基础与插件开发
### 3、自动化测试
  #### 在项目中集成Jest测试框架
  #### 使用Puppeteer构建自动化测试平台
### 4、Docker基础与k8s
  #### Docker基础与k8s基础
### 5、Nginx必知必会
  #### Nginx配置与实战
### 6、Fass与Serverless
  #### Serverless实战
  #### Faas平台搭建
### 7、前端监控系统的搭建
  #### 前端监控体系搭建
  #### 前端性能监控
  #### 前端异常监控
  #### 数据埋点
  #### 监控平台后端架构与开发

### 第一课重点
  `Git与工作流`
    `Git flow`
    `Github flow`
    `Gitlab flow`
    
  `Webpack基础`
  `Lerna包管理`
    `模块管理`
  `微前端 single-spa`
    超大型系统开发痛点
      1、模块之间耦合
      2、模块上线影响范围大
      3、代码合并难
      4、不能并行迭代
      5、沟通成本高
    解决方案
      1、主模块与子模块分离
      2、独立开发
      3、独立部署
      4、独立运行

### 第二课重点
  #### webpack 原理
    Webpack 热更新
  #### Webpack Module Federation
  在客户端或服务器上动态运行另一个 bundle 的代码。
  `动态` 按需，一个包拆开来加载其中一部分
  `运行时` 浏览器里运行，非node编译
  `另一个 bundle 的代码` 应用级 export 成员共享
  `Remote` 被 Host 消费的 Webpack 构建
  `Host` 消费其他 Remote 的 Webpack 构建
  #### Webpack 插件开发
  `compiler`
  `compilation`
  #### Babel 基础与插件开发
  `Babel 是一个 JavaScript 编译器。把最新版的javascript编译成当下可以执行的版本`
  #### TreeShaking
  `Dead Code`
    1、代码不会被执行，不可到达
    2、代码执行的结果不会被用到
    3、代码只会影响死变量(只写不读)
  `ES6 module 特点`
    1、只能作为模块顶层的语句出现
    2、import 的模块名只能是字符串常量
    3、import binding 是 immutable 的
  `Side-effect 副作用`
    在函数式编程中，如下的行为被称之为副作用
    1、修改一个变量
    2、修改一个对象的字段值
    3、抛出异常
    4、在控制台显示信息、从控制台接收输入
    5、在屏幕上显示（GUI）
    6、读写文件、网络、数据库
  1、Rollup 只处理函数和import/export 变量
  2、JavaScript 动态语言特性使得分析比较困难
  3、Side Effect 广泛存在

### 第三课重点
  #### 微前端应用
  #### 微前端原理
  #### shadowDom 和 WebComponents
  `Import map`
    UI组件库构建 组建打包
    模块名映射
    兜底方案：CDN加载失败时加载本地
    内嵌模块
    作用域
    虚拟化
    动态加载
  `System.js`
    SystemJS 是一个插件化的、通用的模块加载器，它能在浏览器或者NodeJS动态加载模块，并且支持 CommonJS、AMD、全局对象模块和ES6模块
  `Single-spa demo`
    微服务
      解耦合
      复用
      服务注册与发现
      RPC
    微前端
      子应用注册
      子应用生命周期
      子应用是怎么控制路由？
      应用之间如何通信
    Single-spa 子应用状态管理
    single-spa 事件
    single-spa 状态管理
  `Qiankun-demo`
    三合一：single-spa sandbox import-html-entry
    HTML entry
    JS 隔离
    Sandbox
    CSS隔离
    Shadow DOM
      影子DOM，潜藏在黑暗中的 DOM 结构
      Shadow-dom 具有良好的密封性
      shadow host: 宿主元素
      shadow root: shadowDom 根节点
      Contents: 内容
  `WebComponents`
    组件化："高内聚，低耦合"，对内各个元素彼此紧密结合、相互依赖，对外和其他组件的联系最少且接口简单。

### 第四课重点
  #### 微前端
  #### Nginx配置详解
    Nginx 架构 异步非阻塞方式 惊群现象
    Nginx 配置
      worker_processes: Work 进程数量，一般设置为核心数。work_processes auto
      worker_connections:  `(Worker 进程数量 × 单个 Worker 进程的最大连接数) / 2`
    http 块配置
    反向代理: proxy_pass
    负载均衡: upstream
      内置策略: 轮询、权重、ip_hash
      扩展策略: fair、url_hash
    rewrite
  #### k8s简介
  #### Docker基础
    镜像(Image)
    容器(Container)
    仓库(Repository)
  容器管理
  `使用docker container command`
  镜像管理
  `使用 docker image command`
  常用命令
  `docker build –t hub.docker.com/nginx:1.0.1 . --build-arg env=$env`
  `docker run --rm -it -d hub.docker.com/nginx:1.0.1 –p –v`
  `-d 后台运行`
  `-it 可交互, 有终端`
  `--rm 容器停止后自动删除`
  `-p [宿主机端口:容器端口]         #端口映射`
  `-v [宿主机目录:容器内目录]。  #挂载存储卷`
  应用场景
  `构建`
  `运行`
  `挂载目录`
  `暴露端口`
  `查看日志`
  `镜像内外文件拷贝`
  `镜像导入`
  #### 前端工程化系统搭建