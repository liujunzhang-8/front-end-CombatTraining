## 前端基本功

### 1、JavaScript 基础
  `基本类型`
    undefined、 null、 boolean、 number、 string、 object、 symbol
  `引用类型`
    Boolean、Number、String、Symbol、Object、Array、Map、Set
  `原型`
    __proto__ 隐式原型，指向构造该对象的构造函数（constructor）的原型（prototype）
    prototype 显示原型，指向函数的原型对象
  `对象创建方法`
    instanceof
    isPrototypeOf
  `原型链遍历`
    hasOwnProperty()
    Object.keys()
    JavaScript 中唯一两个处理属性并且不会遍历原型链的方法
### 2、BOM
  `location`

  `navigation`
    通过 useragent 获取手机品牌型号
    clipboard 粘贴图片
    clipboardData.getData("text/plain") 文字内容
    clipboardData.items 通过item.type 判断内容的类型
    H5 地图定位：Navigation.Geolocation.getCurrentPosition()
    mediaDevices WebRTC Real-Time Communications
    实时通讯技术，它允许网络应用或者站点，在不借助中间媒介的情况下，建立浏览器之间点对点的连接，实现视频流和音频流或着其它任意数据的传输
    Web worker
    基于web worker，独立于 JavaScript 主线程的独立线程，不会堵塞主线程
    在 web worker 的基础上增加了离线缓存能力
    充当服务器与浏览器之间的代理服务器，可以拦截全站的请求，并作出相应的动作。
    支持推送
    可以控制管理缓存的内容以及版本
  `screen`
  `history`
  `performance`
  `window`
  `生成随机数`
  `Proxy`
    Proxy 对象用于创建一个对象的代理，从而实现基本操作的拦截和自定义（如查找属性、赋值、枚举、函数调用等）
  `Reflect`
  `indexedDB`
    浏览器提供的本地数据库，支持事务、索引
    事务是用途？
    事务中一系列的操作要么全部成功，要么一个都不成功，保证原子性和一致性
### 3、DOM

  `尺寸和定位`
    尺寸：style.width、getComputedStyle、offsetWidth、clientWidth、getBoudingClientRect
    定位：offsetTop、offsetLeft
  `Fragment`
    document.createDocumentFragment() 避免频繁大量的dom操作，提升性能
  `高性能DOM编程`
    减少重排、批量修改DOM、事件委托(Event Delegation)
 
### 4、CSS
  `Flex`
    Flex: 一维布局，只能处理一个维度上的元素布局，一行或者一列
  `Grid`
    Grid：布局是将容器划分成了"行" 和 "列"，产生了一个个的网格
  `盒模型`
    W3C 标准盒模型：box-sizing: content-box
    怪异盒模型：box-sizing: border-box
  `预处理器技术`
    变量、嵌套、混合(mixin)、继承(extend)、运算、函数
  `Polyfill`
    浏览器兼容
  `Postcss`
    CSS后处理器框架
    Autoprefixer
    postcss-pxtorem

### 5、底层技术
  `浏览器缓存`
    强制缓存
    协商缓存
  `浏览器渲染`

### 6、正则表达式
  `元字符`
  `字符集合`
  `量词`
  `分支`
  `重复`
  `选择`
  `字符集合`
  `反义`
  `分组`
  `贪婪与懒惰`
  `后向引用`
  `零宽断言`
  `平衡组`
### 7、数据结构与算法基础
  `排序算法`
  `字符集合`

### 第三课重点
  `数据结构与算法`
    链表、树的遍历、二叉搜索树
  `模板引擎实战`


### 第四课重点
  `PWA离线缓存`
  `JavaScript运行原理及内存管理`
  `模板引擎 & Reactivity`