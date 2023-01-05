## Node.js

### 一、Node.js 基础
`输入输出`、`文件系统`、`网络通信`、`进程管理`、`系统模块`

### 二、应用服务器框架开发
`路由`、`视图`、`模型`、`服务`、`从0打造应用服务器框架`

### 三、客户端工具开发
`客户端工具开发`、`脚手架`、`视频流录制`

### 四、数据库技术应用
`关系型数据库应用`、`非关系型数据库`、`前端监控体系后台开发`

### 五、同构和SSR服务端渲染
`SSR服务端渲染`

### 六、网络通信
`https`、`http/2`、`http/3`

### 七、Socket 和 SSE
`Socket 和 SSE`、`视频会议`、`terminal`

### 八、通用中间件应用
`队列 bull`、`缓存 redis`、`消息 kafka`、`定时任务`

### 九、Faas与Serverless
`Faas平台搭建与应用`、`Serverless平台搭建与应用`

### 十、运维与监控
`运维与监控`

### 第一课重点
`Node.js 基础`
  输入输出：
  文件系统：
    Stream 有四种流形式：可读操作；可写操作；可读可写操作；操作被写入数据，然后读出结果
    Pipe 管道
  系统模块：
    OS模块
    全局对象
    path模块
    事件 EventEmitter
    Buffer
    process
    vm模块
    定时器
    crypto
  进程管理：
    子进程：exec、spawn、fork
  网络通信：
    net.Socket：通常用于创建一个 TCP 或本地服务器

### 第二课重点
  `应用服务器框架功能概览`
    express、koa、fastify、next
    路由、视图、模型、服务、中间件、拦截器、数据库、缓存、队列、定时任务、日志、socket
  `Fastify 和 Nest功能实现分析`
    fast-json-stringify: 通过 schema，加速系列化 2x faster than JSON.stringify()
    对象复用：对象池，减少创建时间
    Nest：完美支持 TypeScript、面向AOP编程、支持 Typeorm、Node.js版的 Spring、构建微服务应用
    守卫：控制请求是否由进入路由处理程序处理
    拦截器：在函数执行之前/之后绑定额外的逻辑、转换从函数返回的结果、转换从函数抛出的异常、扩展基本函数行为、根据所选条件完全重写函数（例如,缓存目的）
    管道：在调用控制器的路由处理程序之前，会插入一个管道，管道先拦截方法的调用参数，进行转换或者验证处理，然后用转换好或是验证好的参数调用原方法。
  `中间件使用简介`
    路由、log、queue、redis、mysql、mongodb、websocket、elastcsearch、schedule
    MongoDB 是通用、基于文档的分布式数据库
    redis：主从模式、哨兵sentinel模式、cluster模式
  `装饰器`
    Decorator
  `依赖注入/控制反转`：IOC
  `客户端工具开发`：脚手架@kidi/cli、mongo-init
  `脚手架`
  `GraphQL`
    核心思想：传统的API调用一般获取到的是后端组装好的一个完整对象，而前端可能只需要用其中的某些字段，大部分数据的查询和传输工作都浪费了。GraphQL提供一种全新数据查询方式，可以只获取需要的数据，使API调用更灵活、高效和低成本。
    特点：
      1、需要什么就获取什么数据
      2、网络开销低，可以在单一请求中获取REST中使用多条请求获取的资源
      3、API无需定义各种路由，完全数据驱动
      4、无需管理API版本，一个版本持续演进
      5、强类型Schema
      6、特别适合图状数据结构的业务场景

### 第三课重点
  `Node.js 进程高级应用`
    孤儿进程、僵尸进程、守护进程、进程池、共享内存
  `打造应用服务器框架`
    middleware
  `SSR服务端渲染`
    服务端渲染：
      利：SEO time-to-content 更快的内容到达时间
      弊：服务端开销
      替换方案：预渲染、离线缓存
    初始化：
      SSR 应用会在Node启动时初始化一个renderer单例对象，renderer对象由vue-server-renderer库的createBundleRenderer函数创建，函数接收两个参数，serverBundle（服务端入口文件打包后的）内容和options配置
      获取到serverBundle的入口文件代码并解析为入口函数，每次执行实例化Vue对象
      实例化了render和templateRenderer对象，负责渲染Vue组件和组装HTML
    渲染阶段：
    内容输出阶段
    客户端阶段
  `Serverless`
    Serverless = server + less
    FaaS: Function as a Service Amazon Lambda, Google Cloud Function
    BaaS: Backend as a Service  文件存储、数据库、实时通信、API
    PaaS: Platform as a Service 阿里云、百度云、腾讯云、各种云
    SaaS: Sofeware as a Service 在线办公、视频会议
