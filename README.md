# git 使用那些事儿


工欲善其事，必先利其器，git是一个开源的分布式版本控制工具,很多文章都写的太长，或者资料太多，难以一时间看完。在此总结了git的一些使用方式，因此该文不是鸿篇巨著，但是如果看完也应该可以上手操作了。

## git 安装与配置

> 安装

    Linux: shell 界面输入， sudo  apt-get install git-core 回车输入密码

    Windows：[下载安装包](https://github.com/git-for-windows/git/releases/tag/v2.6.3.windows.1>) 
    下载对应的exe安装包，双击安装

    Mac：terminal : brew install git

> 配置全局用户名和邮箱，Linux: shell ，Windows: Git Bash ，Mac:terminal 命令如下：

    git config --global user.name “wakaka" /user.email "wakaka@gmail.com”
 
> 查看是否配置成功：

    git config --global user.name / user.email

## 创建代码仓库（Repository）

仓库是用于保存版本管理所需信息的地方,所有本地提交的代码都会被提交到仓库中，也可以推送到远程仓库中。比如本地有一个Demo项目，cd进入Demo目录。**输入git init，目录下会生成隐藏的.git文件夹**，如果要删除仓库，删除该文件夹。

## git命令

> add：把要提交的代码添加进来，可以认为到一个缓冲中**[重要]**

    提交文件test.java ：git add test.java

    提交目录test ：git add test

    提交所有文件： git add .

> commit：add完成后，真正的代码提交**[重要]**

    git commit -m “commit” // -m 描述信息，不能为空

> .gitignore: git会检查是否存在该文件，存在就读取该文件内容，将配置文件或者目录排除在版本之外，文件和目录可以使用“\*”通配符。可以手动创建在文件。

    TestA.java // 排除该文件

    testDir // 排除该目录

> status: 查看上次提交后文件修改的列表

    git status

> diff：查看文件修改的内容，-号代表删除部分，+号代表添加部分

    git diff TestB.java // 查看TestB.java修改的内容

> checkout：撤销未提交的修改（未执行add操作）

    git checkout TestB.java // 撤销TestB.java的修改

> reset：取消add状态

    git reset HEAD TestB.java // 取消TestB.java的add状态

> log：查看提交记录（内容包含提交id,提交人，提交日期，描述信息）

    git log // 所有记录

    git log xxxxx(id) -1 // 查看当前id的记录，-1表示一行记录

    git log xxxxx(id) -1 -p // 查看当前id提交记录的修改

## git 分支

分支：可以在现有代码上拉出一个分支，使得代码可以在主干与分支同时开发，并且代码之间互相不会影响。常见使用环境，就是每次版本发布，
已发布的可以拉出一个分支，剩下的功能继续在主干开发，如果发布版本有问题，只用修改分支，最终将代码合并到主干。

> 分支命令：

    git branch -a // 查看所有分支，master主干，分支前有*号，表示当前处于那个分支

    git branch release1.0 // 创建release1.0分支，

    git checkout release1.0 // 切换到release1.0分支，主要与文件修改撤销的区别

    git checkout master // 1： 切换到主干

    git merge release1.0 // 2： 将release1.0的修改合并到master，如果有冲突解决冲突

    git branch -D release1.0 // 删除release1.0分支

## 远程版本库

> 比如有远程版本库，[https://github.com/FreeSunny/RefreashTabView.git](https://github.com/FreeSunny/RefreashTabView.git)

    git clone https://github.com/FreeSunny/RefreashTabView.git // 下载到本地

### 远程库命令：

> push：将代码修改和提交同步到远程库**[重要]**

  git push origin master //origin 指定远程版本库的 Git 地址，master 指定同步到哪一个分支上

> fetch：远程库的修改同步到本地, 不会将代码合并到任何分支，会存放到一个origin/master分支上

    git fetch origin master // 注释同上

> diff：查看远程库修改内容

    git diff origin/master // 注意有一个斜线，就是fetch同步后放置的位置

> merge：将origin/master分支修改的内容合并到主分支

    git merge origin/master // 注意斜线

> pull：fetch + merge，拉取并且合并**[重要]**

    git pull origin master // 没有斜线

## 实例操作[gitbub网址](https://github.com/)

知易行难，say easy than do， 下面就来一个小小的实例，**必须要有git账号**，这个步骤就不用say了吧！

### 创建远程库 

     a. 点击+号下的New repository 创建一个远程库，命名为GitOperate,

     b. 版本库类型可以public或者private，程序员都有开源的心，那就public。

     c. 还可以勾选Initialize this repository with a README，

     d. 接下来可以选择添加.gitignore文件，.gitignore文件有很多类型可以选，
        比如 Android，Android项目下的bin这些文件一般都不需要提交。 
        选择遵循的协议。eg：Apache License 2.0, 这个可以自己去查查每种的意思

     e. 点击create，远程版本库就创建完成了，远程版本库的地址为
        https://github.com/FreeSunny/GitOperate.git。
        之后跳转到README.md,该文件主要是对项目的描述。

### 远程库克隆到本地

     a. 本地创建一个GitOperate文件夹

     b. 远程库地址为https://github.com/FreeSunny/GitOperate.git，
        cd进入GitOperate，输入 *git clone https://github.com/FreeSunny/GitOperate.git*

     c. 完成后可以在GitOperater文件下的GitOperate文件夹下看到README.md文件（两层文件夹了）

     d. 将第二个目录下的所有文件全部复制到上一层目录中，这样就只有第一层目录添加到版本控制中。
        操作命令为(cp -r GitOperate/ .)

### 提交代码

    git add .// 将提交的代码添加进来，这里指README.md

    git commit -m “add readme” // 本地提交

    git push origin master //  同步到远程库

[1]: https://github.com/git-for-windows/git/releases/tag/v2.6.3.windows.1

### 本地已经有文件夹
    
    cd existing_folder //进入已有文件夹
    
    git init // 初始化
    
    git remote add origin  https://github.com/FreeSunny/GitOperate.git //关联远程库
    
    git add .
    
    git commit -m "Initial commit"
    
    git push -u origin master
    
