# 工作中用到的技术详解
1. 持续集成：Jenkins
	1. 什么是Jenkins？
		- Jenkins是一款开源 CI&CD 软件，用于自动化各种任务，包括构建、测试和部署软件。  
			\-- [Jenkins用户手册](https://jenkins.io/zh/doc/)
	2. 关于持续集成：[《转》内容全部转载自阮一峰老师博客](http://www.ruanyifeng.com/blog)
		1. 什么是持续集成？
			>[持续集成指的是，频繁地（一天多次）将代码集成到主干。](http://www.ruanyifeng.com/blog/2015/09/continuous-integration.html)
		2. 持续集成步骤
			1. 提交：开发者向代码仓库提交代码
			2. 测试（第一轮）：代码仓库对commit操作配置了钩子（hook），只要提交代码或者合并进主干，就会跑自动化测试。（我们还没使用到）
			3. 构建：我们用到Jenkins的地方。
				>所谓构建，指的是将源码转换为可以运行的实际代码，比如安装依赖，配置各种资源（样式表、JS脚本、图片）等等。
			4. 测试（第二轮）：第二轮是全面测试，单元测试和集成测试都会跑，有条件的话，也要做端对端测试。所有测试以自动化为主，少数无法自动化的测试用例，就要人工跑。
			5. 部署
			6. 回滚
2. 版本管理：Git
3. 构建工具：Maven
4. 应用服务器：Apache Tomcat7
5. 负载均衡与反向代理：Nginx
6. 框架：SpringMvc、SpringAop、SpringDataRedis、SpringTask