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
  
### 第四课重点
  `应用服务器框架中间件`
    TypeORM
      定义Entity
      获取链接：createConnection
      获取仓库：connection.getRepository(entity)
      增删改查
    MongoDB
      连接：初始化client
      获取集合：createConnection
      增删改查
    Kafka
      连接：初始化client
      获取生产者：getProducer
      创建Topic：createTopics
      创建消息：send
      获取消费者：getConsumer
      添加Topic：createTopics
      监听消息：on
    Redis
      连接：初始化client
      增删改查
    Elasticsearch
      连接：初始化client
      增删改查
  `TCP & UDP`
    TCP
      数据包
        以太网数据包（packet）的大小是固定的，最初是1518字节，后来增加到1522字节。其中，1500字节是负载（payload），22字节是头信息（head）。
      数据传输
        数据包编号
        ACK
        慢启动
        TCP协议为了做到效率与可靠性的统一，设计了一个慢启动（slow start）机制。开始的时候，发送得较慢，然后根据丢包的情况，调整速率：如果不丢包，就加速发送速度；如果丢包，就降低发送速度。
    UDP
      面向无连接
        不需要在发送数据前进行三次握手建立连接的，想发数据就可以开始发送了。并且也只是数据报文的搬运工，不会对数据报文进行任何拆分和拼接操作。
      支持单播多播广播
        支持一对多，多对多，多对一的方式
      面向报文
        发送方的UDP对应用程序交下来的报文，在添加首部后就向下交付IP层。UDP对应用层交下来的报文，既不合并，也不拆分，而是保留这些报文的边界。因此，应用程序必须选择合适大小的报文
      不可靠性
        无连接，不会备份数据，不会关心对方是否已经正确接收到数据
      头部开销小
        UDP的头部开销小，只有八字节，相比TCP的至少二十字节要少得多，在传输数据报文时是很高效的
    SSL自签名证书
      生成CA私钥
      生成csr文件
      生成自签名证书
      生成带有ca签名的证书
  `HTTP HTTP/2 HTTP/3`
    HTTPS
      HTTP协议以明文的方式发送内容，不提供任何方式的数据加密
      HTTPS在HTTP的基础上加入了SSL协议，SSL依靠证书来验证服务器的身份，并为浏览器和服务器之间的通信加密。
      HTTP+SSL/TLS
      SSL（Secure Socket Layer，安全套接字层）
      TLS（Transport Layer Security，传输层安全）
      HTTPS 的缺点
        HTTPS协议多次握手，导致页面的加载时间延长近50%
        HTTPS连接缓存不如HTTP高效，会增加数据开销和功耗
        申请SSL证书需要钱，功能越强大的证书费用越高
        SSL涉及到的安全算法会消耗CPU资源，对服务器资源消耗较大
    HTTP2
      Server Push
        Non-push加载耗时
        RTT + max(RTT, size(HTML)/BandWidth) + size(JS)/BandWidth
        push加载耗时
        RTT + size(HTML)/BandWidth + size(JS)/BW
        所以决定推送是否有改善性能的衡量因素是 size(HTML/BandWidth)和 RTT 谁大
      优点：
        HTTP/2 采用二进制格式而非文本格式
        HTTP/2是完全多路复用的，而非有序并阻塞的，只需一个连接即可实现并行
        使用报头压缩，HTTP/2降低了开销
        HTTP/2让服务器可以将响应主动"推送"到客户端缓存中。
    HTTP3
      QUIC (Quick UDP Internet Connections) 快速UDP互联网连接
      QUIC的次要目标包括减少连接和传输延迟，在每个方向进行带宽估计以避免拥塞。它还将拥塞控制算法移动到用户空间，而不是内核空间，此外使用前向纠错（FEC）进行扩展，以在出现错误时进一步提高性能
      队头阻塞
      ORTT 建链
        HTTPS：TCP握手和TLS握手至少2-3个RTT
        DH(Diffie-Hellman)迪菲-赫尔曼算法 密钥交换
      QUIC 协议
        首次连接，客户端和服务端要使用1RTT进行密钥交换
      非首次连接
        实现ORTT的业务数据交互
      连接迁移
  `Nodejs微服务`
    功能模块独立，减少模块间依赖和耦合
    模块单独部署，服务隔离
    服务注册与发现
    服务间通讯
      HTTP
      TCP
      消息：Redis、Kafka
      RPC：gRPC
        HTTP/2 + PB
        通信协议基于标准的HTTP/2设计，支持双向流、消息头压缩、单TCP的多路复用、服务端推送等特性，这些特性使得gRPC在移动端设备上更加省电和节省网络流量。
      ProtoBuf
        足够简单
        序列化后体积很小
        解析速度快
        多语言支持
        更好的兼容性

    ZooKeeper注册与发现
      `Node.js网关`
        API网关是微服务架构中的一种服务，它为客户端提供共享层和API，以便与内部服务进行通信。API网关可以进行路由请求、转换协   议、聚合数据以及实现共享逻辑，如认证和速率限制器。API网关是微服务世界的入口点。
        认证
        数据汇总
        序列化格式转换
        协议转换
      `网络应用`
        Socket
          WebSocket
            WebSocket 是应用层第七层上的一个应用层协议，它必须依赖HTTP协议进行一次握手，握手成功后，数据就直接从TCP通道传输，与HTTP无关了。即：WebSocket分为握手和数据传输阶段，即进行了HTTP握手 + 双工的TCP连接。
            传输阶段
              WebSocket的数据传输是frame形式传输的，比如会将一条消息分为几个frame，按照先后顺序传输出去。
              frame（帧）是WebSocket发送数据的基本单位。
          socket.io
            封装了WebSocket和轮询等方法，可以做到很好的兼容。
        SSE
          基于HTTP协议，使用流信息Streaming向浏览器推送消息
          WebSocket：全双工通道，可以双向通信。
          SSE：是单向通道，只能服务器向浏览器发送
          SSE使用HTTP协议，现有的服务器软件都支持
          WebSocket是一个独立协议
          SSE属于轻量级，使用简单
          WebSocket协议相对复杂
          SSE默认支持断线重连
          WebSocket需要自己实现
          SSE一般只用来传送文本，二进制数据需要编码后传送
          WebSocket默认支持传送二进制数据
          SSE支持自定义发送的消息类型