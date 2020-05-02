### axios
  官网:http://www.axios-js.com/zh-cn/docs/
  安装:npm install axios
  axios发送请求的7种基本形式:
      直接使用axios
        import axios from "axios"
          axios(config)
          axios(url,config)
              config中的url不用再填了
          axios.get(url,config)
              config中的url method不用再填了
      使用axios实例(以后我们在大型项目开发中 可以一个模块一个实例)
        import axios from "axios"
          const axiosIns = axios.create(config)
          axiosIns()

          const axiosIns = axios.create()
          axiosIns(config)

          const axiosIns = axios.create()
          axiosIns(url,config)

          const axiosIns = axios.create()
          axiosIns.get(url,config)


  axios配置的优先级 (从上往下优先级依次递增)
      全局的 axios
      自定义实例
      请求时的配置
          axios.defaults.baseURL="http://www.a.com"
          const appAxios = axios.create({
            baseURL:"http://www.b.com"
          })
          appAxios.get("/damu",{
            baseURL:"http://www.c.com",
          })


  axios拦截器
      共性的:
        请求拦截器的第一个回调 : 请求发送之前 对请求的配置做一些补充
        响应拦截器的第一个回调 : 对请求回来的数据做一次整理
        响应拦截器的第二个回调 : 错误处理

      为一个axios实例配置拦截器; 不管以后这个实例发多少个请求 拦截器都会启作用
      为axios函数 配置拦截器; 不管以后这个axios函数发多少个请求 拦截器都会启作用

      async mounted(){
          const appAxios = axios.create({
            baseURL:"http://localhost:9000/api2"
          });

          //为appAxios定义拦截器
          // 添加请求拦截器
          appAxios.interceptors.request.use(function (config) {
            config.headers.Authorization = "damu";
            return config;
          });

          // 添加响应拦截器
          appAxios.interceptors.response.use(function (response) {
            return response.data;
          }, function (error) {
            console.log(error,"---")
            return Promise.reject(error);
          });



          const body = await appAxios.get("/contactList")
          console.log(body)
      }


### restful风格的后台接口
    早期CRUD接口:
        C: /contact/create
        R: /contact/red
        U: /contact/update
        D: /contact/delete
    restful规范
        C: /contact; method:post
        R: /contact; method:get
        U: /contact; method:put
        D: /contact; method:delete
        http响应状态码的语义:
            https://koa.bootcss.com/#response