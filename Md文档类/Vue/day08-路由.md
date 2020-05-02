## 路由
### 普通路由
    学会路由的基本使用
        1. 定义路由组件 (pages文件夹)
        2. 定义路由 (本质上就是一个数组 [{路由的配置...},{},{}])
        3. 定义路由器
            --- 将路由注册成插件
            --- 将路由交给路由器管理
        4. 将路由器交给vue管理
        5. 路由的跳转要靠 router-link
        6. 路由组件的渲染要靠 router-view(一级路由;要在一级组件App中进行渲染)
### 嵌套路由
        {
            path:"/home",
            component:home,
            children:[
              {path:"news",component:news},
              {path:"message",component:message}
            ]
        }
        1. 分清你的路由是几级路由 应该在哪个组件中进行渲染
        2. 嵌套路由的path不能加/
### 动态路由
        动态路由的本质: 多个结构类似的path会命中同一个路由组件
            第一种配法:{path:"/user/:id",component:user},
            第二种配法:{
                        path:"/user",
                        component:user,
                        children:[
                          {path:":id",component:userDetail},
                        ]
                      }
        动态路由的注意点
            组件的复用:
                /user/1 --> user组件
                /user/2 --> user组件
                在导航进行切换时;动态路由组件是不会被重新加载的;动态路由组件对应的生命周期钩子是不会被触发的
                解决方案:
                    watch $route
            动态路由组件传参
                任何一个组件中都可以访问到$route这个对象;可以直接在组件上使用
                    $route.params(path中的params /:id)
                    $route.query (path中的query  ?name=damu&age=18)
                让组件与$route进行解耦
                    路由中有个props的配置
                        props:true
                        props:{}
                        props:route=({})

                        把对应的数据通过类似于父向子传值的形式交给对应的路由组件;
                        路由组件就可以通过props来接收

### 声明式导航 & 编程式导航
    声明式导航:router-link


### 路由器的配置
    routes:注册路由
    mode:路由的模式 (hash,history)
      hash模式;兼容性比较高;可是不实用;在一些支付场景中不支持;在生产环境中不能使用
      history模式;兼容性没有hash好;但比较实用;在一些需要和后台交互的场景下;需要使用history模式
    linkActiveClass: 对path进行模糊匹配 匹配到之后 为对应的router-link渲染的a标签 加对应的class
    linkExactActiveClass:对path进行精确匹配 匹配到之后 为对应的router-link渲染的a标签 加对应的class
### 路由的配置
    path:路径
    component:路径对应的组件
    redirect :路由重定向
    children:嵌套路由
    props:路由组件传参