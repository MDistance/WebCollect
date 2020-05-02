### vue的其他技术点
    过渡动画的api
        在vue中使用 v-if/v-show时; 结合transition组件  vue会自动为transition组件中使用
        v-if/v-show的节点;加必要的class.
            当节点从离开状态 --> 显示状态时
                v-enter (要不要以v-开头 得观察transition的name属性)
                v-enter-active
                v-enter-to
            当节点从显示状态 --> 离开状态时
                v-leave(这个api是废的 issue#3580)
                v-leave-active
                v-leave-to

    ref
        <div ref="damu"></div>
            vm.$refs.damu : dom节点
        <v-damu ref="damuC"></v-damu>
            vm.$refs.damuC : vue组件
    表单元素的值如何收集
        v-model; 根据表单类型的不同 我们要使用不一样的数据类型来收集表单数据
    过滤器
    自定义指令
    插件
        定义插件: 定义一个具有install方法的对象
        使用插件: Vue.use(对象)
            当前对象的instal方法 会被vue自动调用 而且的一个参数是Vue构造


### 简单的使用脚手架 能让项目跑起来
    npm i vue-cli -g
    vue list
    vue init webpack projectName
    进入到项目目录:
        npm start

        改端口 改主机
        set PROT=3000
        set HOST=127.0.0.1
        npm start


### 如果你想在面试时;在vue脚手架这一块比较出彩;或者说相对脚手架有一定的深层次了解
    1. vue的完整版本&vue的运行时版本的区别
        区别在于 能不能使用template
    2. render函数的语法
        render(h){return h(组件配置对象)}
        render(h){return h(标签,数据)}
    3. 对webpack比较熟悉;了解webpack的基本配置;熟悉webpack的包查找机制

