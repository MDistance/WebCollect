### css sticky footer
    html:
        <div id="app">
            <div class="mainWrap">
                <div class="main">

                </div>
            </div>
            <div class="footer">
                footer
            </div>
        <div>
    css:
        .mainWrap{
            min-height: 100%;
            .main{
                overflow:hidden; //清除浮动
                padding-bottom: 60px;
            }
        }
        .footer{
            margin-top: -60px;
            height: 60px;
        }

### stylus
    不需要{}不需要:不需要;
    混合定义:
        one-px()
            css 声明
    混合使用:
        one-px()
    继承定义:
        .clearfix
             css 声明
    继承使用
        @extend .clearfix

### 项目功能
    头部+遮罩布局
