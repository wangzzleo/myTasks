目前项目中Redis使用的场景：
1. 分布式锁：
  使用redisson 或者 SpringDataRedis
  场景：1）集群系统进件时，以唯一性数据为锁key。
             2）定时任务  ：自定义注解 TaskHandle，两个值：value（锁名称），expireTime（锁过期时间），使用aspectj 作为aop框架。
2. 暂时未使用热点数据缓存
