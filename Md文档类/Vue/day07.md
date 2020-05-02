### 使用脚手架创建项目;读懂项目启动的流程

### 拆分静态组件;将一个静态页拆成vue的组件
        有多少个组件
        组件与组件之间的关系
               App
                   todo-header
                   todo-list
                        todo-item
                   todo-footer

### 设计数据结构;以及数据初始化的位置
        todolist案例 我们的数据结构: [{},{}]
        数据初始化的位置: App中 (因为header,list,footer都要使用到这份数据)

### todolist的业务逻辑
       header:
            新增待办任务的业务逻辑:  涉及到header 向 app 传递数据(item;待办任务)
       list&item:
            删除待办任务的业务逻辑:
                涉及到item 向 app 传递数据(id,删除那一项的id)
            选中完成一个待办任务的业务逻辑:
                要注意v-model的脏数据(使用计算属性的set方法);
                涉及到item 向 app 传递数据(id选中的id,选中状态)
            vue中对样式的使用:
                操作class : 完成类似于hover的效果
                操作style :  控制删除按钮的显示隐藏
       footer:
            清除已完成任务(涉及到footer 向 app进行一次通信)
            全部数据&已完成数量(计算属性的使用!!!)
            全选&全不选功能(计算属性 get&set; 涉及footer 向 app传递数据(全选按钮的状态))
       数据持久化