# ajax 假数据库
---

https://git.ms.netease.com/fe/mockjax/tree/master

### 当前库列表
---

- jquery-mockjax [默认]
> 复杂数据模拟推荐使用

	本地文档： https://git.ms.netease.com/fe/mockjax/tree/master/jquery-mockjax
	
- mock
> 简单快捷  
> `注意`：不能使用本库映射url，因为与fe/ajax不兼容。  
> 但可以用于动态生成假数据。  
   
    支持jquery zepto 配置插件还可支持angular  
    在线文档： http://mockjs.com/  

### 假数据说明
---

> ajax假数据使用示例：  
> `注意`：前端代码无需标明依赖假数据文件，由ftl直接作为入口文件引入。  
~~~
<@docFoot js = [ "./main.js" ] mockjax = ["./mock.ajax.js"] />
~~~

> 标准的假数据入文件写法 mock.ajax.js  
> `注意`：只能使用$.mockjax映射url  
~~~js
require(['jquery', 'mockjax'], function($) {
	// 一般这样写
	$.mockjax({
		url: "/user/all",
		responseTime: 1500,
		responseText: {
			list: [
				{ id: 1, name: '王炜毅'},
				{ id: 2, name: '梁峰'}
			]
		}
	});
	// 可以使用mock.js库 Mock.mock()动态生成假数据
	// 但不能使用mock.js库的url映射，因为与fe/ajax不兼容
	$.mockjax({
		url: "/user/list",
		responseText: Mock.mock({
			'list|2-13': [
				{ 
				    'id': '@id',
				    'name': '@name()',
			        'login': '@boolean(1, 9, true)'
				}
			]
		})
	});
})
~~~