### 搭建项目的开发环境
    axios的二次封装(难点) post-packaging;


### vue项目中发送ajax请求的流程
    1. 安装axios npm i axios
    2. 将src下的util文件 & http文件拷贝一份贴入到项目中
    3. 配置模块的请求
    4. 将 http/模块名/index.js暴露的对象 挂载给 http/index.js
    5. 将 http/index.js  暴露的对象 挂载给 main.js
    6. 组件上使用的形式
            async function (){
                await this.$http.模块名.key(data)
            }

    axios 二次封装的api
        拷贝http下的一个文件夹
        http/模块名/axios.js http/模块名/index.js 都不用动
        修改http/模块名config.js
            往外暴露一个对象;对象的属性即为配置
                  api: 对象;这个配置是项目发送ajax请求最核心的配置;对象的键值对代表一个请求
                        key 就是以后组件上发送ajax请求的async函数的名字;key自主命名
                        key:{
                              url:"/contactList",   //代表请求的地址
                              method:"get",         //代表请求的方法
                              toast:true,           //代表请求时是否需要轻提示
                              data:{a:"a"},         //请求时携带的静态数据
                              isForm:true,          //请求时的参数 要使用form-data的形式
                              hooks:{               //单个请求级别的钩子
                                beforeReq(){},                 //在请求发送之前要处理的一些个性化逻辑
                                afterReqSuccess(body){},       //在请求发送成功之后要处理的一些个性化逻辑
                                afterReqFail(){},              //在请求发送失败之后要处理的一些个性化逻辑
                              }
                        }
                  baseUrl: //当前模块请求的基地址
                  timeout: //当前模块请求的超时时间
                  name   : //当前模块的名字
                  hooks:{: //模块级别的钩子
                    beforeReq(){},          //在请求发送之前要处理的一些模块级别共性的逻辑
                    afterReqSuccess(data){},//在请求发送成功之后要处理的一些模块级别共性的逻辑
                    afterReqFail(){},       //在请求发送失败之后要处理的一些模块级别共性的逻辑
                  }





