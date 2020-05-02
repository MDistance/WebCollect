### 实现左右列表的联动
    1. 获取到右侧列表 滑到每一项时的位置 记录成一个数组
    2. 获取右侧列表实时位置
        var test = new BScroll(dom,{probeType:3});
        test.on("事件名",()=>{})
            scroll
                参数：{Object} {x, y} 滚动的实时坐标
                触发时机：滚动过程中，具体时机取决于选项中的 probeType。
    3. 通过前两步得到的数据 动态计算左侧哪一个li应该被选中
    4. 让左侧列表中选中的那个li出现在视口区域中(尽量往头上顶)
            var test = new BScroll(dom);
            test.scrollToElement(el, time)
    5. 点击左侧列表 让右侧列表滑动到指定区域