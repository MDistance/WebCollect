### 学习js的技巧
    1. 要弄清楚js api是用来干嘛的
    2. 观察这个js api的参数
    3. 观察这个js api的返回值

### 学习css的技巧
    1. 要弄清楚这个css属性是用来干嘛的
    2. 观察这个css属性的默认值
    3. 观察这个css属性是否可继承
    4. 如果这个css属性值存在百分比;那么这个百分比参照于谁

### css复习
    flex相关
        两组核心概念: 容器&项目  主轴&侧轴
        Flex布局的精髓: 处理等分&等比例布局
            容器上的属性:
                flex-direction
                flex-wrap
                flex-flow
                justify-content
                align-items
                align-content(只有在flex-wrap不为no-wrap启作用)
            项目上的属性
                order
                align-self
                flex-shrink
                flex-grow
                flex-basis
                flex:1 (简写属性)
                    flex-grow:1
                    flex-shrink:1
                    flex-basis:0%

    字体图标(基于自定义字体)
        iconfont
            依赖于阿里的
        iconmoon
            自己拿矢量图生成一套字体图标

    BFC
        规则
            1.内部的Box会在垂直方向，一个接一个地放置。(块级元素独占一行)
            2.BFC的区域不会与float box重叠。(两列布局)
            3.内部的Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠
            4.计算BFC的高度时，浮动元素也参与计算。(清除浮动)
        生成条件
            1. 根元素
            2. float属性不为none
            3. position为absolute或fixed
            4. overflow不为visible
            5. display为inline-block

    css预处理器
        变量
        嵌套
        混合(混合相比于继承 更加的灵活;因为可以传参数 项目中使用的更多 )
        继承(比较高性能 选择器的组合 并不是样式的复制 一些固定不变的公共样式应该要定义成继承)
            选择器:extend(className all)
        css模块化

    css后置处理器
        postcss: 用来对css文件 进行兼容性处理的(基于can i use这个站点)
        不用去记postcss的配置 只需要明白postcss是用来做什么的进行
        因为后期 我们会有脚手架 所有的配置都是一键生成的



### ECMAScript
    ES开发 比较重要的两个编程思想
        函数化编程
        异步编程: 区分开回调函数的注册 与调用
            注册(线程池中的异步线程把回调放到异步队列中去的那个过程)
            调用(v8引擎最终来执行)

    ES6异步的最佳实践:
        如何生成一个Promise实例?
            new Promise(执行器)
                默认情况情况下 返回的是一个pending状态的promise
                当前promise的状态如何改变 得看执行器的执行过程
                    如果执行器函数的第一个参数被调用 当前这个promise会变成成功状态
                    如果执行器函数的第二个参数被调用 当前这个promise会变成失败状态
                    如果执行器函数在执行时报错      当前这个promise会变成失败状态
            promise.then ; promise.catch
                默认情况情况下 返回的是一个pending状态的promise
                当前promise的状态如何改变 得看then或catch的回调执行结果
                    如果回调返回一个值 当前这个promise会变成成功状态
                    如果回调在执行时出现异常 当前这个promise会变成失败状态
                    如果当前这个回调返回一个promise 当前这个promise跟返回的promise保持一样的状态
            async函数的返回值
                默认情况情况下 返回的是一个pending状态的promise
                当前promise的状态如何改变 得看async函数执行结果
                    如果async函数返回一个值 当前这个promise会变成成功状态
                    如果async函数在执行时出现异常 当前这个promise会变成失败状态
                    如果async函数返回一个promise 当前这个promise跟返回的promise保持一样的状态

        如何正确的使用Promise
            1. 执行器内部一定得有异步代码 而且执行的两个参数 一定是在异步的函数中调用的
            2. then中的回调一般都应该返回一个promise

        async&await
            合理的使用async&await
                await 等的一定是一个promise对象
                要灵活的使用async函数返回的那个promise