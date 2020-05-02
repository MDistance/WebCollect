### html复习
    template : 模板标签; 这个标签中的内容初始化的时候不会被渲染
    html标签的属性:
        所有html标签的属性 它的值都是字符串
    attr&prop:
        都是对html属性的一个抽象
        attr: 标签的预定义属性 & 标签的自定义属性
            修改attr的api : node.setAttribute(attrName,value)
        prop: 标签的预定义属性
            修改prop的api : node.propname = value
        重点讨论prop中的布尔值属性
            修改布尔值属性的prop 是 不会同步其attr的
            修改布尔值属性的attr
                在没有动过其prop的前提下 是会同步prop的
                一旦动了prop 是不会同步prop的
            浏览器认prop
            用户操作的也是prop
        凡是对布尔值属性做操作;我们应该统一修改其prop;尽量避免操作attr

### css复习
    选择器有关:
        选择器的读取顺序
            浏览器是从右往左读的

        两个需要注意的选择器:
            nth-child(index)
            nth-of-type(index)
            以上两个选择器
                index都是从1开始的!!!
                #wrap > .item:nth-child(2)以child为中心;
                        肯定是去找一个父元素底下的第2个子节点 要让第二个子节点满足一定条件才会选中
                #wrap > p:nth-of-type(2)以type为中心;
                        找#wrap底下第二个p标签

        声明的优先级:
            样式表由什么组成?
                规则
                    选择器+声明块
                            一个个合法的css属性键值对

            层叠(声明优先级的规则)
                首先按来源进行区分
                    用户的重要声明
                    开发者的重要声明
                    开发者的普通声明
                    用户的普通声明
                    用户代理的声明
                如果来源区分不开 按选择器的特殊性
                    选择器的特殊性 按 a,b,c,d 来区分的; 而且选择器的特殊性是不会进位的
                        0,0,0,0 : *
                        0,0,0,1 : 元素选择器 (p,div,span)
                        0,0,1,0 : 类选择器   (.item,.wrap)
                        0,1,0,0 : id选择器   (#app)
                        1,0,0,0 : 内联样式
                如果选择器的特殊性区分不开 按顺序

    定位&盒模型有关
        对前端坐标系有个(理解
            前端坐标系 会随着使用的css属性不一样 而产生改变

        绝对定位的参照物: 包含块
            对于一个绝对定位的元素 其包含块查找的规则:
                离它最近的开启定位的祖先元素;如果没有则找到初始包含块;
                初始包含块是一个视窗大小的矩形(默认情况下 位置与视窗一致)

        滚动条
            系统滚动条
                滑动系统滚动条;会使初始包含块的位置产生移动
            普通元素的滚动条
                滑动普通元素的滚动条;会使元素内部的标签位置产生移动
            overflow
                当html 和 body 只有一个元素拥有overflow属性时;该属性控制的是系统滚动条
                当html 和 body 都有一个元素拥有overflow属性时;
                    html的overflow属性控制的是系统滚动条
                    body的overflow属性控制的是body的滚动条

        绝对定位盒模型的特点
            横向上盒模型相关的尺寸 + left + right = 包含块横向的padding-box的尺寸
            纵向上盒模型相关的尺寸 + top + bottom = 包含块纵向的padding-box的尺寸

    flex相关
        两组核心概念: 容器&项目  主轴&侧轴
            容器上的属性:
                flex-direction
                flex-wrap
                flex-flow
                justify-content
                align-items
                align-content(只有在flex-wrap不为no-wrap启作用)