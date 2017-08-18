# myPrivateProject
In this project, some java notes and  paragraph of codes were saved for my locating.

<!DOCTYPE html>
<html>
 <head>
  <title>实现Ajax异步交互</title>
  <meta charset="utf-8" />
 </head>

 <body>
  <input type="button" value="异步请求" id="btn">
  <script>
	// 实现Ajax的异步交互的步骤
	
	var btn = document.getElementById("btn");
	btn.onclick = function(){
		/*
		 * 1. 实现Ajax主要依靠XMLHttpRequest对象
		 *   * 创建XMLHttpRequest对象
		 */
		var xhr = getXhr();
		/*
		 * 2. 与服务器端建立连接
		 *   * open(method,url,async)方法
		 *     * method - 设置当前的请求类型(GET或POST)
		 *     * url - 设置当前的请求地址
		 *     * async - 设置是否异步(Boolean类型)
		 *       * 默认值为true,表示异步
		 *       * 官方认为使用XMLHttpRequest对象就是为了实现异步交互的
		 */
		xhr.open("get","01.php?user=zongwr");
		/*
		 * 3. 客户端向服务器端发送请求
		 *   * send(请求参数)方法
		 *     * 请求参数的格式 - key=value
		 *   * 如果请求类型为GET方式的话
		 *     * send()方法是不能向服务器端发送请求数据的
		 *   * 注意
		 *     * send()方法是不能被省略的
		 *       * GET请求类型 - send(NULL);
		 */
		xhr.send(null);
		/*
		 * 4. 客户端接收服务器端的响应
		 *   * 使用onreadystatechange事件
		 *     * 监听服务器的通信状态
		 *   * readyState属性
		 *     * 得到服务器端当前通信状态
		 *     * 备选项
		 *       * 0 尚未初始化
		 *       * 1 正在接收
		 *       * 2 接收完成
		 *       * 3 正在响应
		 *       * 4 响应完成
		 *   * status - 状态码
		 *     * 200 OK
		 *   * responseText属性
		 *     * 接收服务器端的数据(HTML格式)
		 */
		xhr.onreadystatechange = function(){
			// 保证服务器端响应的数据发送完毕
			if(xhr.readyState == 4){
				// 保证这次请求必须是成功的
				if(xhr.status == 200){
					// 接收服务器端的数据
					var data = xhr.responseText;
					// 测试
					console.log(data);
				}
			}
		}
	}

	
	// 定义创建XMLHttpRequest对象的函数
	function getXhr(){
		// 声明XMLHttpRequest对象
		var xhr = null;
		// 根据不同浏览器创建
		if(window.XMLHttpRequest){
			// 其他浏览器
			xhr = new XMLHttpRequest();
		}else{
			// IE浏览器(8及之前)
			xhr = new ActiveXObject("Microsoft.XMLHttp");
		}
		// 返回XMLHttpRequest对象
		return xhr;
	}
  </script>
 </body>
</html>



<?php
	// 用于处理客户端的Ajax异步请求
	// 1. 接收客户端发送的请求数据
	$user = $_GET['user'];
	// 2. 向客户端进行响应
	echo $user.' get request succesful.';
?>
