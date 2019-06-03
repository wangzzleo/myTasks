1.  获取锁时 ：SETNX key， EXPIRE  key seconds
      释放锁时 ：DELETE key
```
tryLock(){  
    SETNX Key 1
    EXPIRE Key Seconds
}
release(){  
  DELETE Key
}
```
  - 优点：
    简单，给锁加过期时间可以避免应用异常或者重启导致锁无法释放。
  - 缺点：
    每次提交一个命令，如果SETNX后应用异常、重启，尚未设置过期时间就会出问题。可以使用lua脚本改善。但是如果执行SETNX后Redis crash或者发生主从切换，依然会出现问题。

2. 