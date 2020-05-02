### vue路由环境的搭建(直接写在main.js中)
  1. 将vue-router定义成插件
  2. 定义路由组件
  3. 定义路由
  4. 定义路由器
  5. 将路由器挂载给根实例


### vue 路由环境的搭建(工程化的写法,建议!!!)
  1. 定义路由组件
      pages
  2. 定义路由(将路由组件 与 一个路径相映射)
      routes
  3. 定义路由器
      router
        将vueRouter定义成vue的插件
        将路由注册到vueRouter中
  4. 将路由器交给vue管理
  5. 最终路由组件的跳转依赖于 router-link组件
  6. 最终路由组件的显示依赖于 router-view组件

### vue-router学习的大纲
  普通路由
    注意整个vue-router使用的流程
  嵌套路由
    注意路由的命名规范
  动态路由
    普通路由组件进行切换时;整个路由所对应的组件是会被销毁并重新创建的
  声明式导航&编程式导航

  路由器的配置
    routes:注册路由
    mode:路由的模式 (hash,history)
      hash模式;兼容性比较高;可是不实用;在一些支付场景中不支持;在生产环境中不能使用
      history模式;兼容性没有hash好;但比较实用;在一些需要和后台交互的场景下;需要使用history模式
    linkActiveClass: 对path进行模糊匹配 匹配到之后 为对应的router-link渲染的a标签 加对应的class
    linkExactActiveClass:对path进行精确匹配 匹配到之后 为对应的router-link渲染的a标签 加对应的class
  路由的配置
    path:路径
    component:路径对应的组件
    redirect :路由重定向
    children:嵌套路由
    props:路由组件传参


