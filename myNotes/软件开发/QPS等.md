# QPS、TPS、PV、RT等

1. RPS = 每秒请求数 （requests per second）
  
	

2. PV = 指页面被浏览的次数，比如你打开一网页，那么这个网站的pv就算加了一次（page view）

	

3. TPS = 每秒内的事务数，是衡量系统性能的一个非常重要的指标(transactions per second)。
一个事务是指一个客户机向服务器发送请求然后服务器做出反应的过程。

4. QPS = 每秒内查询次数，比如执行了select操作，相应的qps会增加（queries per second）。在因特网上，作为域名系统服务器的机器的性能经常用每秒查询率来衡量。

5. 并发用户数：指的是现实系统中操作业务的用户，在性能测试工具中，一般称为虚拟用户数(Virutal User)，注意并发用户数跟注册用户数、在线用户数有很大差别的，并发用户数一定会对服务器产生压力的，而在线用户数只是 ”挂” 在系统上（我理解是session的个数？），对服务器不产生压力，注册用户数一般指的是数据库中存在的用户数。

6. RT = 响应时间