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
  8、Vue需要Fiber吗？
    1、更新去重
    2、依赖收集
    3、准确定位需要更新组件
  9、Vite
    `创建项目`
      yarn create vite-app hellovite
    `特性`
      快速的冷启动
      即时的模块热更新
      真正的按需编译、
    `主要流程`
      1、浏览器import请求
      2、Vite dev Server 中间拦截
      3、请求地址处理
      4、@vue/compiler-sfc编译Vue
      5、返回结果处理
      6、浏览器运行
    `Vite HMR热更新`
      服务端
        `文件改变监听`
        `找到依赖这个文件的vue`
        `相关的Vue重新编译`
        `编译结果和缓存结果对比`
        `变化发送到客户端`
        `更新缓存`
      客户端
        `vue`: reload、rerender
        `style`: 更新、移除
        `js-update`: 更新
        `full-reload`: window.reload 刷新页面
    浏览器里运行ES module 时大势所趋
    HTTP/2 HTTP/3 普及能解决模块请求的性能问题
    Vite的思想将彻底改变工程化构建
  10、插槽
    组件化的灵魂是组件，插槽是组件复用的灵魂
    `默认插槽`、`具名插槽`、`作用域插槽`
    父组件模板解析在子组件之前，所以父组件首先会获取到插槽模板内容
    子组件模板解析在后，子组件调用render方法生成Vnode时，可以拿到插槽的Vnode节点
    作用域插槽可以获取子组件内变量，因此作用域插槽的Vnode是根据scope动态生成的
    作用域插槽与普通插槽相比，主要区别在于插槽内容可以获取到子组件作用域变量。由于需要注入子组件变量，相比于具名插槽，作用域插槽有以下几点不同
      `作用域插槽在组件渲染方法时，生成的是一个包含注入作用域的方法，相对于createElement生成Vnode，多了一层注入作用域方法包裹，这也就决定插槽Vnode作用域插槽是在子组件生成Vnode时生成，而具名插槽是在父组件创建Vnode时生成`
      `子组件初始化时会处理具名插槽节点，挂载到组件$slots中，作用域插槽则在renderSlot中直接被调用`
  11、组件间通信
    `方法一：props $emit`
    `方法二：ref $children $parent`
    ref：如果在普通的DOM元素上使用，引入指向的就是DOM元素；如果用在子组件上，引用就指向组件实例。
    $parent / $children：访问父 / 子实例
    `方法三：EventBus ($emit / $on)`
    通过一个空的Vue实例作为中央事件总线(事件中心)，用它来触发事件和监听事件，从而实现任何组件间的通信，包括父子、隔代、兄弟组件。
    `方法四：$attrs / $listeners`
      $attrs: 包含了父作用域中不被prop所识别(且获取)的特性绑定，可以通过v-bind="$attrs"传入内部组件。
      $listeners: 包含了父作用域中的(不含.native修饰器的)v-on事件监听器。它可以通过v-on="$listeners"传入内部组件
    `方法五：Vuex`
      每一个Vuex应用的核心就是store(仓库)。"store" 基本上就是一个容器，它包含着你的应用中大部分的状态(state)
      Vuex的状态存储是响应式的。当Vue组件从store中读取状态的时候，若store中的状态发生变化，那么相应的组件也会相应地得到高效更新
      改变store中的状态的唯一途径就是显式地提交(commit) mutation。这样使得我们可以方便地跟踪每一个状态的变化。
    `方法六：provide / inject`
      1、init 时调用initInjections获取inject项
      2、resolveInject，遍历所有的parent，寻找provide
      3、给Inject项添加响应式处理
  12、全局API
    `Vue.extend(options)`: 使用基础Vue构造器，创建一个"子类"
    `Vue.nextTick([callback, context])`: 在下次DOM更新循环结束之后执行延迟回调
    `Vue.set(target, propertyName/index, value)`: 向响应式对象添加一个属性，并确保这个新属性同样是响应式的，且触发视图更新
    `Vue.delete(target, propertyName/index)`: 删除对象的属性。如果对象是响应式的，确保删除能触发更新视图
    Object.defineProperty 无法监测对象属性的增加和删除，无法比较好处理数组元素变化。所以有了这些全局方法。
    `Vue.directive(id, [definition])`: 注册或获取全局指令
    `Vue.filter(id, [definition])`: 注册或获取全局过滤器
    `Vue.component(id, [definition])`: 注册或获取全局组件，使用给定的id设置组件的名称
    `Vue.use(plugin)`: 如果插件是一个对象，必须提供install方法。如果插件是一个函数，它会被作为install方法。install方法调用时，会将Vue作为参数传入。
    当install方法被同一个插件多次调用，插件将只会被安装一次。
    `Vue.mixin(mixin)`: 全局注册一个混入，影响注册之后所有创建的每个Vue实例。插件作者可以使用混入，向组件注入自定义的行为。不推荐在应用代码中使用。
    `Vue.compile(template)`: 在render函数中编译模板字符串。只在独立构建时有效。
    `Vue.observable(object)`: 让一个对象可响应。Vue内部会用它来处理data函数返回的对象。
    `Vue.version`: Vue安装版本号
  13、Vue3原理解析
    `响应式API`
      reactive：reactive 用于为对象添加响应式状态。接收一个js对象作为参数，返回一个具有响应式状态的副本。参数只能传入对象类型
      ref：ref的本质是拷贝，与原始数据没有引用关系
      toRef：toRef的本质是引用，与原始数据有关联
      toRefs：作用其实和toRef类似，只不过toRef是一个个手动赋值，而toRefs是自动赋值
      对比：
        ref本质是拷贝，修改响应式数据不会影响原始数据
        toRef的本质是引用关系，修改响应式数据会影响原始数据

        ref数据发生变化，界面会自动更新
        toRef当数据发生改变时，界面不会自动更新

        toRef传参与ref不同
        toRef接收两个参数，第一个参数是哪个对象，第二个参数是对象的哪个属性
      readonly
        获取一个对象(响应式或纯对象)或ref并返回原始代理的只读代理。只读代理是深层的：访问的任何嵌套property也是只读的
      shallowReactive
        创建一个响应式代理，该代理跟踪其自身property的响应性，但不执行嵌套对象的深度响应式转换(暴露原始值)
      watch
        watch侦听特定的data源，并在单独的回调函数中副作用。默认情况下，它也是惰性的。
      watchEffect
        在响应式地跟踪其依赖项时立即运行一个函数，并在更改依赖项时重新运行它
      computed
        给computed函数传递一个getter方法创建immutable reactive ref object
        给computed函数传递一个有get和set方法的对象来创建一个writable ref object
      effect
        接受一个函数，返回一个新的监听函数reactiveEffect。若监听函数内部依赖了reactive数据，当这些数据变更时会触发监听函数。
        effect 作为reactive 的核心，主要负责收集依赖，更新依赖
          每次effect执行返回的都是全新的监听函数，即使传递的相同的函数
          对响应数据的原始数据的操作，不会触发监听函数
          通过stop api，终止监听函数继续监听
        effect如何收集依赖
          track
            检查当前激活的activeEffect
            检查targetMap中有没有当前target
            没有则添加一个target，然后创建一个depMap
            depMap里添加依赖
            get、has、iterate 三种类型的读取对象会触发track
        effect在执行的时候会在取值之前将自己放入到effectStack栈顶，同时将自己标记为activeEffect，以便进行依赖收集与reactive进行关联
        在取值的时候开始收集依赖，所以需要在取值之前将依赖的effect放到栈顶并标识为activeEffect，执行effect回调取值的时候会在Proxy的handlers的get中进行取值，所以我们需要在这里进行依赖收集
        需要在Proxy类的handlers的set中触发依赖的执行
        每次effect执行，都会重新将当前effect放到栈顶，然后执行effect回调再次取值的时候，再一次执行track收集依赖，不过第二次track的时候，对应的依赖集合中已经存在当前effect了，所以不会再次将当前effect添加进去了。
    `组合式API`
      为什么要有组合API？
        更好的逻辑复用与代码组织
        更好的类型推导
  14、组件开发实战
    `TypeScript`
      类型申明：
        1、基本类型
        2、数组类型
        3、枚举类型
        4、元组
        5、Any任意类型
        6、Void无类型
        7、联合类型
        8、交叉类型
      类型断言：
        类型断言不是类型转换
        欺骗了ts编译器，不进行特殊的数据检查和解构，运行js的时候还是可能报错的
      类型保护：
        开启了strictNullChecks，则不能直接调用变量可能为null的变量上的方法和属性
      泛型：
        泛型是对类型进行编程，可以提高代码的重用性和代码的通用性
    `Vue3组合API`
    `组件开发`
      `CSS变量`
        声明一个自定义属性，属性名需要以两个减号(--)开始
      `currentColor`
        currentColor表示当前的标签所继承的文字颜色
      `父子组件通信 provide/inject`
      `响应式 provide/inject`
      `props 类型/检验`
      `space`
        renderSlot($slots, 'default', {key: 0}, () => [])
        创建节点
        h(标签, {属性}, 内容)
        h(标签, {属性}, [可以继续嵌套h()])
        createVNode(标签, {属性}, 内容)
        createVNode(标签, {属性}, [可以继续嵌套createVNode()])
        createVNode()函数的功能比h()函数要多且做了性能优化，渲染节点的速度也更快
