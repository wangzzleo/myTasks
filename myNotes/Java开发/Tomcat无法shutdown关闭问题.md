1. 环境：Tomcat 7、java version "1.8.0_144"、dubbo2.5.7等
2. 使用jstack分析线程状态：[命令详解]([https://www.cnblogs.com/kongzhongqijing/articles/3630264.html](https://www.cnblogs.com/kongzhongqijing/articles/3630264.html)
)
3. waiting on condition:等待区等待、被park
注意：
>>runnable:状态一般为RUNNABLE。
>>in Object.wait():等待区等待,状态为WAITING或TIMED_WAITING。
>>waiting for monitor entry:进入区等待,状态为BLOCKED。
>>waiting on condition:等待区等待、被park。
>>sleeping:休眠的线程,调用了Thread.sleep()。

入手点总结
wait on monitor entry： 被阻塞的,肯定有问题
runnable ： 注意IO线程
in Object.wait()： 注意非线程池等待