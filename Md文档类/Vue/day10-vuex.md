### vuex
    学习vuex;关注的两个核心点:
        1. 怎么优雅安全的读取仓库中的数据
        2. 怎么优雅安全的修改仓库中的数据
    学习vuex;关注的两个核心规律(大部分情况下)
        1. 仓库中的数据在组件上都应该有一个计算属性与之对应
        2. 仓库中操作数据的工具在组件上都应该有一个方法与之对应
            在结合v-model的时候;仓库中操作数据的工具在组件上由一个set方法与之对应
    vuex的配置项:
        vuex的配置项都会装绑给我们仓库实例对象
        在vuex环境中 每个组件都可以访问到$store(仓库实例)
        数据仓库:
            state:{
                a:"a",
                b:b
            }
        对仓库中的数据进行组合;仓库内部的计算属性
            getters:{
                msg(state){
                    return state.a + "-" + state.b
                }
            }
        同步修改仓库数据的工具
            mutations:{
                add(state){
                    state.a="a2"
                }
            }
        异步修改仓库数据的工具
            actions:{
                asyncAdd(store){
                    store.commit("mutationname")
                }
            }
    vuex使用流程
        组件上去dispatch一个action
        action中会发送异步请求;在请求成功之前得到数据;commit一个mutation
        mutation会同步的去修改仓库中的数据;devtools会记录下每一次mutation的操作
        仓库中的数据被改变;组件得到响应式更新
    vuex的优化
        仓库级别的优化
        组件上的优化
            vuex提供了mapState,mapGetters,mapActions,mapMutations这些辅助函数;
            让组件的写法变的简洁