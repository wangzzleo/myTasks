# HttpClient 使用

##使用步骤
1. 创建 HttpClient 对象
2. 创建请求方法实例。
	1. POST请求，创建HttpPost对象
	2. GET请求，创建HttpGet对象
3. 设置请求参数
	- HttpPost 使用setEntity方法设置请求参数。

4. 调用HttpClient的execute方法，以第2步创建的实例为参数。该方法会返回HttpResponse对象。
5. 使用第4步返回的HttpResponse对象的方法获取响应信息。
6. 调用HttpClient的close方法关闭连接。
