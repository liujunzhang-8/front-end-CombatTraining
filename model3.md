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
  `Fastify 和 Nest功能实现分析`
  `中间件使用简介`