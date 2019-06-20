hui # 我的待探究疑问

## 已完成

1. 在阅读周明耀老师的《深入理解JVM ＆ G1 GC》该书时，对本书p31~33关于String的部分内容产生疑问，遂通过google等搜索引擎以及Stack Overflow和知乎(R大)[https://www.zhihu.com/people/rednaxelafx/answers?order_by=vote_num]的解答研究了一番，最终理解还是有欠缺，所以抽时间专门研究了一下这个问题。  
[从intern函数产生的疑问](https://www.jianshu.com/p/10b5a7702e63)

3. git reset & revert区别    
git revert是通过新增commit的方式恢复到之前的版本，而reset则是通过撤销之前的commit方式恢复之前的版本。
4. rebase & merge的区别  
同样是合并分支效果，rebase把分叉的提交历史“整理”成一条直线，看上去更干净直观。 merge则老老实实的交待发生的事情，feature分支的提交和合并过程都会作为commit显示。 

5. git pull & git pull --rebase区别  
   git pull做了两个操作分别是pull和merge。所以加了rebase就是以rebase的方式进行合并分支，默认为merge。

2. git fetch & pull 区别  
pull会主动merge远程仓库与本地仓库代码，fetch需要手动merge。git fetch origin master -> git log -p FETCH_HEAD -> git merge FETCH_HEAD  == git pull



## 待完成

1. 使用JDK自带的JAXB进行Java对象和XML转换时```Feature 'http://javax.xml.XMLConstants/feature/secure-processing' is not recognized.```。我的疑问：按照双亲委派机制，应该会先到JDK路径找的吧，为什么会先加载扩展包的实现类呢？  
2. Maven 正常打包，调用时候报NoSuchMethod。打包时依赖jar的module与打包的项目处于Intellij IDEA的同一级project下面。

