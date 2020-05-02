### 如何修改windows的环境变量
    set : 查看当前windows操作系统所有的环境变量
    set name : 查看指定的环境变量的值
    set name=val : 设置环境变量(一次性的 关闭命令行窗口后 当前的设置就会失效)
    set name= : 删除环境变量

### vue脚手架2.0
    安装脚手架:
        npm install -g vue-cli
            npm 帮你生成了脚手架对应的命令
                vue,vue-init,vue-list
            命令存放的目录 被配置在了环境变量的path中

    查阅一下脚手架可支持的模板
        vue list
        可以查到 template-name

    使用脚手架生成项目(以下命令得运行在项目的包裹目录下)
         vue init <template-name> <project-name>

    启动项目
        npm run dev
        npm start

### 脚手架启动流程基本分析
    启动的是开发环境:
        1. 启动开发服务器
            npm start
            npm run dev
            webpack-dev-server --inline --progress --config build/webpack.dev.conf.js
                webpack-dev-server : 脚手架内置一个开发服务器
                --inline --progress : 将脚手架的启动进度在一行进行显示

        2. 查看开发服务器对应的配置文件
                公司的脚手架工具 可能会要去环境变量中读取一些信息;
                我们要学会使用set命令(windows 操作系统的命令) 来操作环境变量
                build/webpack.dev.conf.js:
                    //process node的内置模块;用来读取操作系统的一些信息
                    //process.env : 读取操作系统中环境变量
                    const HOST = process.env.HOST
                    const PORT = process.env.PORT && Number(process.env.PORT)
                    const merge = require('webpack-merge');
                    const baseWebpackConfig = require('./webpack.base.conf');
                    const config = require('../config')
                    const devWebpackConfig = merge(baseWebpackConfig,{
                        devServer:{
                            host: HOST || config.dev.host,
                            port: PORT || config.dev.port,
                            open: config.dev.autoOpenBrowser
                        }
                    });


        3. 启动项目后;界面是如何出来的?
                build/webpack.base.conf.js
                    entry:{
                         app: './src/main.js' // 整个项目的入口!!!
                    }
                    output: {
                        filename: 'app.js',
                    }
                    new HtmlWebpackPlugin({
                      filename: 'index.html',
                      template: 'index.html',
                      inject: true
                    }),
                    打包成功之后的文件:
                        new Vue({
                          el: '#app',
                          template: '<div id="app">
                                      <span>test</span>
                                    </div>'
                        })

### vue的源码版本
      完整版本 : 编译器 + 运行时 ; 支持template
      运行时版本:    不支持template

### render
    配置项:
        render:function(h){
            //return h("span","123");
            return h(组件的配置对象);
        }

### webpack找包的机制
    https://webpack.docschina.org/concepts/module-resolution
    import App from "./App";
        经过vue-loader的处理 我们拿到的就是app组件的配置对象
    import Vue from "vue";
        webpack找到的到底是一个什么样的文件?
            webpack import的规则?
                import Vue from "vue";

                配别名的情况: "vue"是一个别名!!
                    直接找别名指定的文件

                沒有配别名的情况: "vue"是一个包!!
                    1. 根据resolve.modules这个配置去指定的目录中查找vue这个包
                    2. 找包的描述文件package.json
                    3. 根据resolve.mainFields 去package.json找对应的字段
                    4. 如果以上步骤没有找到对应的js文件 则按照resolve.mainFiles字段指定的文件名 去找对应的文件
                    5. 文件的扩展名 由resolve.extensions来决定
                    6. 如果以上步骤都没有成功  那么webpack就找不到对应的包!

