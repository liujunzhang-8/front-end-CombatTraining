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
    `数组`
      Proxy能完美的解决数组的监听检测问题，数组push、unshift、splice等不同方法，都能很好的拦截处理
    `对象`
      对象增加属性，删除属性，都能很好的拦截
    `Proxy一共有13种拦截操作`
      get、set、has、ownKeys、apply、construct、preventExtensions、isExtensible、deleteProperty、defineProperty、getPrototypeOf、setPrototypeOf、getOwnPropertyDescriptor
    每个组件实例都有相应的 watcher 实例对象，它会在组件渲染的过程中把属性记录为依赖，之后当依赖项的setter被调用时，会通知 watcher 重新计算，从而致使它关联的组件得以更新
    `observe`
      遍历data中的属性，使用 Object.defineProperty 的 get/set 方法对其进行数据劫持
    `dep`
      每个属性拥有自己的消息订阅器 dep，用于存放所有订阅了该属性的观察者对象
    `watcher`
      观察者（对象），通过 dep 实现对响应属性的监听，监听到结果后，主要触发自己的回调进行响应。
    `Watcher 和 Dep 的关系`
      watcher 中实例化了 dep 并向 dep.subs 中添加了订阅者，dep 通过 notify 遍历了 dep.subs 通知每个 watcher 更新
  3、Watcher
    每个组件实例都对应一个 watcher 实例，它会在组件渲染的过程中把 "接触" 过的数据 property 记录为依赖。之后当依赖项的 setter 触发时，会通知 watcher，从而使它关联的组件重新渲染
  4、Vue版本
    `Runtime Only`
    `Runtime + Compiler`
    `Weex runtime`
    `Webpack`: vue-loader 对.vue进行编译
    `Compiler实时编译模板`
  5、挂载过程
  6、模版编译
    `vue-template-compiler`
    `HTMLParser` ——→ `ElementAST` ——→ `AST optimize` ——→ `Generate Code`
    `HTMLParser`
      开始标签，入栈
      结束标签，出栈
    `AST optimize`
      optimizer的目的就是虚拟DOM对比时的剪枝。主要就是遍历一棵树，为静态子树标记tag
    `Codegen`
      Codegen是一个代码生成器。
      功能是将AST树转化为一个字符串，字符串内容是一段可执行的JavaScript代码
  7、Virtual DOM
    `Vnode`
      用js模拟dom结构
      通过js计算减少dom操作，节省性能
      相对于传统方案全部删除重新渲染，vdom可以做修改前后对比，点对点的更新dom，避免任何多余的dom渲染
      `create` ——→ `diff` ———→ `patch`
      `patch原理`
        patch(oldVnode,vnode,hydrating,removeOnly)
        patch提供了5个生命周期钩子：
          1、create：创建patch时
          2、activate：激活组件时
          3、update：更新节点时
          4、remove：移除节点时
          5、destroy：销毁节点时