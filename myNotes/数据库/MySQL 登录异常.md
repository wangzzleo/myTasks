今天遇到一个问题，耽误了我一早上时间。
昨天快下班时候在我本地数据库执行了个修改root权限的语句，忘记执行什么了，直接复制的，今天早上登录不上去了。
报如下错误：
``` Access denied for user 'root'@'localhost' (using password: YES)```
MySQL版本如下：```Server version: 8.0.14 MySQL Community Server```，Win7系统。
心知是昨天执行root用户权限造成的，原以为使用```mysqld --console --skip-grant-tables --shared-memory```修改密码即可，结果一直报错，反复尝试都不行，最后用管理员权限启动```CMD```，再```cd```到bin目录下面，重新启动终于成功。这儿应该是执行权限问题。
登录成功后```ALTER USER "root"@"%" IDENTIFIED  BY "你的新密码";```修改密码，结果报
```
The MySQL server is running with the --skip-grant-tables option so it cannot execute this statement
```
此时```flush privileges``` 一下就行，
```mysql> flush privileges;```
再次执行上述ALTER命令。修改成功。
接下来关闭```mysqld```，再重启MySQL服务即可```net start mysql80```。