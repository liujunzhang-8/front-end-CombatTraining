## Vue核心技术解析

### 一、Vue核心技术解析
  `响应式原理`、`模板编译`、`虚拟dom`、`插槽`、`事件机制`、`Watch原理`、`内置组件`、`指令`、`Keep-alive`、`nextTick`
### 二、组件化技术对比
  `React`、`高阶组件`、`Hooks`、`Fiber`
### 三、组件动态渲染
  `低代码基础`、`可配置表单`
### 四、Vue3底层原理
  `主要改变&迁移`、`Composite API`
### 五、Vite构建工具
  `底层原理`
### 六、组件库构建实践
  `Element-UI`、`工程化`
### 七、常用组件实现精髓详解
  `Element-UI`
### 八、组件化实战
  `VueCore`、`低代码平台`

### Vue源码概览
  1、Compiler编译器
    `模板解析`、`优化器`、`代码生成`
  2、core核心
    `组件`、`全局API`、`observer`、`实例`、`工具类`、`vdom`
  3、platform核心
    `web`、`compiler`、`runtime`、`server`、`工具类`
    `weex`
  4、server服务端渲染
    `bundle-renderer`、`optimizing-compiler`、`template-renderer`、`webpack-plugin`
  5、sfc单文件组件
    `解析器`
  6、shared共享
    `常量`、`工具类`
  7、_init方法
    `合并options`
    `初始化生命周期`
    `初始化事件`
    `初始化render`
    `生命周期回调beforeCreate`
    `依赖注入`
    `初始化state`
    `初始化provider`
    `生命周期回调created`

### 响应式原理
  1、Object.defineProperty
    descriptor的属性描述符有两种形式，一种是数据描述符，另一种是存取描述符
    `数据描述符`
      configurable：数据是否可删除，可配置
      enumerable：属性是否可枚举
      value：属性值,默认为undefined
      writable：属性是否可读写
    `存取描述符`
      configurable：数据是否可删除，可配置
      enumerable：属性是否可枚举
      get: 一个给属性提供 getter 的方法，如果没有 getter 则为 undefined
      set: 一个给属性提供 setter 的方法，如果没有 setter 则为 undefined
    `数组`
      已知长度的数组的索引操作可以拦截。数组元素添加无法进行拦截，Vue做了特殊处理
    `对象`
      对象属性新增，删除无法拦截
      Vue里使用set
  2、Proxy
    真正在语言层面对数据拦截的定义，解决数组，对象某些情况下无法进行拦截的问题