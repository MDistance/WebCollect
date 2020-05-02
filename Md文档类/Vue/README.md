### 题外话
  自研项目:
        代码是写给人看的;顺便让机器运行一下
        在项目特别复杂的情况下,我们写出来的代码 ,应该也要尽量的易读(便于以后项目的维护;便于以后新增需求)
  外包项目:
    写完就走人;不要我们维护的

### axios的二次封装
    当前版本的缺点:
      请求的代码太冗余;在接口规范不一致的情况下(接口需要的参数可能不同类型的)会导致前端代码特别难以维护;
      业务逻辑很难梳理
    优化后的版本:
      请求是配置化的;自动化的;
      可以抹平传参的差异;不管你接口要什么参数;组件上发请求时只传对象

### axios二次封装的目录设计
    body = await this.$http.contact.createContactByForm({name,tel,id})
    body = await this.$http.user.getUsers()
        //$http对象代表的是项目中所有模块请求需要的方法
        this.$http:{      contact:{                       user:{
          contact,          createContactByForm(){}         getUsers(){}
          user            }                               }
        }


    http
      contact
        axios.js : 提供发送请求的工具给util.http-1.js  被util.http.js引用
        config.js: 提供发送请求的配置给util.http-1.js  被util.http.js引用
        index.js : 暴露contact模块所需要的请求方法组成的对象 被http.index.js引用
      user
        axios.js
        config.js
        index.js : 暴露user模块所需要的请求方法组成的对象 被http.index.js引用
    index.js : 暴露整个项目所需要的请求方法组成的对象


    util
      http-1.js : 返回对应模块请求方法组成的对象 被每一个模块的index.js文件引用

### 实现util.http-1.js
    当前这个js文件 主要是根据axios实例 & config配置对象 来生成对应的请求方法组成的对象

### 同学练习时的几个问题
    1. vue中发请求的方式 与 react中发请求的方式 是两种模式
            vue中是基于axios进行二次封装
            react中只是拿一个函数包裹了一下
    2. export default fn()
            往外暴露的不是一个函数 而是函数的执行结果
    3. import user from "@/user"
            如果user是一个目录 那么上述import的方式 相当于import user from "@/user/index.js"
    4. httpUtil函数被调用的次数
            得看http目录的index.js 引入了几个模块
            一定要分析清楚 在axios中做二次封装时;我们所定义的函数 分别是在什么时候被调用的
    5. 回顾代码的时候 看看自己到底写了多少闭包

### 实现loading效果




