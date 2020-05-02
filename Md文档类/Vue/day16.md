### vue中如何解决跨域问题
    1. baseurl不能配置! 应该让我们的请求到达devServer(开发环境) ngix(生产环境)

    2. 在静态资源服务器中配置代理
        跨单域
            vue.config.js
                devServer:{
                    proxy: 'http://localhost:4000'
                }
            对devserve来说 任何的404请求都会被转发到proxy服务器
            对于客户端来说 只需要将请求发到devServer上;baseurl不能配置!
        跨多域
            vue.config.js
                ^:拖字符
                devServer:{
                    '/4000': {
                       target: 'http://localhost:4000',
                       changeOrigin: true,
                       pathRewrite:{
                           "^/4000":""
                       }
                    }
                }
            对devserve来说 去掉域之后以"/4000"开头的404请求都会被转发到proxy服务器
            对于客户端来说 要将请求发给devServer
                而且path前要加上/4000 在真正去代理服务器的时候 把/4000去掉 baseurl不能配置!
                    发请求时加/4000 是config.js中的corsUrl配置处理的
                    去代理时去/4000 是vue.config.js中的pathRewrite配置处理的

    3. devserve在处理请求时的一些细节
            ajax请求是一种特殊的http请求; 它是由xmlhttprequest对象创建的;一般都是浏览器引擎一个模块
            点击一个a标签 去访问一个地址; img标签去访问一个地址; link标签去访问一个css 这些都是http请求;
            不是ajax请求

            如果我们向devServer发送一个http请求!!!这个请求在devServer中没有命中任何静态资源,说明
            当前这个请求就是一个未知请求(404请求)devServe会返回index.html.
            因为这个http请求有可能是前端路由 不是去访问静态资源的,devServe返回index.html之后
            再去请求打包成功之后的js文件 在那个js文件中根据vue-router的配置来显示对应的界面

            如果我们向devServer发送一个ajax请求 而且devserver没有为这个ajax请求配置代理 那devServer
            会返回404

            如果我们向devServer发送一个ajax请求 而且devserver为当前这个ajax请求配置了代理 代理到真正
            的api服务器上去的时候  发现这个api服务器没有对应的后台路由 这个时候devServer会认为自己已经
            处理成功 只是api服务器没有成功  那devsever 会将index.html返回回去