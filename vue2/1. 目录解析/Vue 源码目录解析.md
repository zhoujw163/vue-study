# Vue 架构预览

Vue 源码构建相关配置放在 scripts/config.js 中，定义了代码的输出类型。

    - 输出各模块规范的代码：es module、commmonjs、umd
    - 输出各端的代码：服务端渲染、web、weex
    - 输出 runtime / runtime + compiler 的代码

src 目录结构
    
    - compiler：编译模板，把模板编译 ast 语法树，ast 语法树优化，代码生成等功能。
    - core：vue.js的核心代码，包括内置组件，全局API封装，数据监测，虚拟dom等
    - platforms：平台模块代码（web/weex），对核心代码的补充，各平台有自己的 compiler、runtime、util
    - server：处理服务端渲染
    - sfc：处理 .vue 文件，将 .vue 文件解析成 js 对象。
    - shared：提供共享的工具函数

src/core 目录结构

    - components：存放 keepAlive 组件
    - global-api：给 Vue 添加全局 API（use、mixin、extend...）
    - instance：Vue 初始化（合并配置，初始化生命周期，初始化事件中心，初始化渲染，初始化 data、props、computed、watcher ...）
    - observer：数据的收集和订阅
    - vdom：虚拟dom
    - util：工具函数

总结：Vue.js 的组成是由 core + 对应平台的补充代码构成（独立构建和运行时构建只是 platforms 下 web 平台的两种选择）。

Vue2.0 怎么在实现数据双向绑定的同时引入 Virtual DOM ？
