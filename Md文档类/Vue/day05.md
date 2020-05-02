### vue 配置
    el:
        1. 确定了根组件(new vue)的模板
        2. 确定了根组件(new vue)的挂载节点
    data
        1. 在根组件中可以写成对象
        2. 子非根组件中要定义成一个函数
    methods
    computed
        计算属性比侦听器要自动化;运用起来更加的简单;
        计算属性本身不难;难的是想不到使用计算属性,在我们分析需求的时候;
            当我们遇到一个数据要依赖于其他数据时;我们一定要想到使用计算属性
    watch
        监听data中属性变化的
        watch:{
            监听的data中属性名(val){
                // val 该属性被修改后的值
            }
        }
    components
        用来定义vue中局部组件
        components:{
                    组件名:组件的配置项
                }
    生命周期的钩子
        beforeCreate(){console.log("beforeCreate")},
        created(){console.log("created")},
        beforeMount(){console.log("beforeMount")},
        mounted(){console.log("mounted")},
        beforeUpdate(){console.log("beforeUpdate")},
        updated(){console.log("updated")},
        beforeDestroy(){console.log("beforeDestroy")},
        destroyed(){console.log("destroyed")}
### vue 实例对象
    实例对象身上比较重要的两个点:
        1. data中的属性会转绑给vm实例对象; vm实例对象代理了data中属性的读写
        2. 一个vue组件 就是 一个vm实例对象
                var vue组件 = new vueComponent()
                vueComponent.prototype = Object.create(Vue.prototype)
                ---> 对象级别的继承: vueComponent.prototype.__proto__ = Vue.prototype

                vue组件对象 要去查找自己可以使用的属性 和 方法时 走的是下面这条链
                所有构造函数的显示原型 我们可以认为其是一个Object的实例对象
                    vue组件 --> vue组件.__proto__ --> vueComponent.prototype.__proto__
                            --> Vue.prototype.__proto__ ---> Object.prototype.__proto__
                            --> null

                当一个对象 要去查找自己可以使用的属性 和 方法时;会遵循原型链的规则;
                原型链是隐式原型链;  对象a({}) 查找属性和方法时走的是下面这条链:
                    a --> a.__proto__  --> Object.prototype.__proto__ --> null
    属性:
        $root
        $el
        $options
        $data
    方法:
        $mount(el)
        $set
        $watch
        $destroyed
    事件(vue自定义事件):
        $on
        $emit
        $off
        $once

### vue 组件化
    在vue中;组件分为两大类:
        全局组件
            Vue.component(组件名,组件的配置项)
        局部组件
            components:{
                组件名:组件的配置项
            }
        组件的配置项 vs vue配置项:
            不能写el;
            data得是一个函数!!!
    组件的使用细节
        1. is属性 解决html5标签嵌套的冲突
        2. 在一个组件标签身上 使用@ ;代表给当前这个组件注册了一个vue的自定义事件
        3. props特性 & 非props特性

### 生命周期
    //vue做完界面的初始化
    beforeCreate(){console.log("beforeCreate")},
    created(){console.log("created")},
    beforeMount(){console.log("beforeMount")},
    mounted(){console.log("mounted")},


    //界面更新
    beforeUpdate(){console.log("beforeUpdate")},
    updated(){console.log("updated")},

    //vm被销毁
    beforeDestroy(){console.log("beforeDestroy")},
    destroyed(){console.log("destroyed")}

### 组件间数据的传递
    父向子
        通过子组件标签上的自定义属性  +  props
    子向父
        通过子组件标签上的自定义属性(传递一个函数) + props
        vue自定义事件
    非父子
        总线
        pubsub
