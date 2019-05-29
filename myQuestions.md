# 我的待探究疑问

## 已完成

1. 在阅读周明耀老师的《深入理解JVM ＆ G1 GC》该书时，对本书p31~33关于String的部分内容产生疑问，遂通过google等搜索引擎以及Stack Overflow和知乎(R大)[https://www.zhihu.com/people/rednaxelafx/answers?order_by=vote_num]的解答研究了一番，最终理解还是有欠缺，所以抽时间专门研究了一下这个问题。

[从intern函数产生的疑问](https://www.jianshu.com/p/10b5a7702e63)

## 待完成

1. 使用JDK自带的JAXB进行Java对象和XML转换时候遇到的问题：```Feature 'http://javax.xml.XMLConstants/feature/secure-processing' is not recognized.```根据双亲委派机制，应该会先到JDK路径找的吧，为什么会先加载扩展包的实现类呢？我对双亲委派模型本来就有点迷，更加迷了，改日细细研究一番。
