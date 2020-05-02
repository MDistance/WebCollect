* 搜索电影
	* 接口地址：https://api.douban.com/v2/movie/search
	* 请求方式：GET
	* 请求参数：
		* q=string  要查询的电影名称  例如: https://api.douban.com/v2/movie/search?q=小猪佩奇
		* count=number  返回电影的数量（0-20） 例如: https://api.douban.com/v2/movie/search?count=8&q=小猪佩奇
		* start=number  从第几条开始返回 
	* 返回值：JSON字符串
	* 注意：请求接口有次数限制，约是1分钟/100次（一旦达到上限，半小时后再试）