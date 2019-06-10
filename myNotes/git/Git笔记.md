1. 项目中如果想知道某处代码是谁提交的，可以使用```git blame my_file```,如下：  
![blame演示.png](https://upload-images.jianshu.io/upload_images/13572633-846045895b6765ae.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
也可以指定行：
```
git blame -L 1,5 my_file
```

2. git checkout几个作用
    - 切换或者新建分支
  新建分支 ```git checkout dev```
  新建并检出分支 ```git checkout -b dev```
    - 将暂存区或者指定commit内容覆盖到工作区
暂存区中文件恢复到工作区，多个文件用空格隔开 ```git checkout my_file1 my_file1```
如果要还原所有文件 ```git checkout .```
如果checkout后面是文件名称,最好这样写：``` git checkout -- my_file```，这里的```--```很重要，不加他会变成切换分支的操作。
    - 用指定commit提交的内容覆盖工作区  
1）使用 ```git log``` 查询指定SHA-1值，假如是 ```1a2b3c```
再使用  ```git checkout 1a2b3c -- my_file``` 覆盖my_file文件  
2）或者使用 ```git checkout HEAD^^ -- my_file```，使用上上一个提交版本来覆盖  
3）抑或使用```git checkout dev -- my_file```使对应分支中的文件还原到当前分支的工作区。
3. 使用```git branch -m dev test```可以修改分支名称
4. 使用```git branch -d dev```删除分支后，如果想恢复了，可以使用删除时候 commit对象的sha-1值（假如是 123abcd)再新建一个分支```git branch dev```。
5. HEAD是什么？
HEAD是一个指针，通常情况下，它指向当前所在分支，而分支又指向一个commit提交。
HEAD并不总指向一个分支，某些时候仅指向某个commit提交，这就形成detached HEAD。
6. git reset --hard 会把工作目录的文件恢复到某一次提交的状态，覆盖现在的文件   
git reset --soft 只会移动HEAD指针的位置，不会改变暂存区和工作目录的内容  
7. 删除远程仓库的文件或者目录  
``` git rm -r --cached .idea```  ```-r```为删除目录，不加该参数为删除文件。 ```--cached```删除的是本地仓库中的文件，工作区的文件会保留且不再与远程仓库发生跟踪关系。如果本地仓库中的文件也要删除则无需此参数。之后再commit，push即可。
8. 如果只想merge个别文件或文件夹怎么做？  
8.1 使用```checkout```将分支B部分文件添加到分支A:```git checkout dev -- target_file```，但是要**注意，在使用```git checkout```某文件到当前分支时，会将当前分支的对应文件强行覆盖**。在这时候需要使用下面的方法。
8.2 如果分支A已经有```target_file```文件，可以  
    - 先```git checkout -b A_temp```建临时分支并且换到临时分支
    - 再将分支B```merge```到临时分支```git merge B```，
    - 再切换到分支A```git checkout A```
    - 最后再将对应的```target_file```从临时分支A_temp ```checkout```过来```git checkout A_temp target_file```。

9. 对于已经存在的本地仓库，如何关联上GitHub上的远程仓库？  
    新建GitHub仓库时候已经告诉咱们了：
```
git remote add origin git@github.com:wangzzleo/online.git
git push -u origin master
```

10. 获取远程仓库指定分支内容
	- git pull <远程仓库名> <远程分支>:<本地分支>  
	  如果要与当前分支merge，则不需要写冒号后的本地分支；如果当前分支与目标分支有关联关系，则远程分支名也可以省略。
	- git checkout -b 本地分支名 origin/远程分支名  
	  会创建一个新的本地分支切换过去，并与制定远程分支关联。