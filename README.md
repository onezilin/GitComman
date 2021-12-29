#### 1、【git init】

初始化git仓库

#### 2、【git add 文件名】

将文件添加到暂存区

#### 3、【git commit -m "提交说明"】

将暂存区文件添加提交到git仓库进行版本管理

#### 4、【git log [--oneline] [--graph]】

查看提交的版本，`--oneline`相当于`--pretty=oneline --abbrev-commit`，表示输出格式为一行并且只展示版本的前几位

#### 5、【git reset [--hard | -- mixed | soft] [ HEAD~数字 | 版本号 ]】

`HEAD~数字` 数字回到前几个版本（若只写`HEAD`表示回到当前版本，可以用于重置工作区、暂存区文件），或者回到指定版本，除了未被跟踪的文件不会受影响，其他参数对文件影响如下：

`
--hard `【删除】指定版本中已commit文件在工作区、暂存区和版本之后的修改，指定版本之后的所有文件及其修改；

`
--mixed` 【保存】指定版本中已commit文件在工作区、暂存区和版本之后的修改，指定版本之后的所有文件及其修改。所有在工作区、暂存区的文件返回工作区，指定版本中已commit文件在版本之后的修改都放回工作区，指定版本之后的所有已commit文件变成未被跟踪的文件放在工作区；

`
--soft` 【保存】指定版本中已commit文件在工作区、暂存区和版本之后的修改，指定版本之后的所有文件及其修改。所有在工作区、暂存区的文件仍在工作区、暂存区，指定版本中已commit文件在版本之后的修改都放回暂存区，指定版本之后的所有已commit文件变成未被跟踪的文件放在暂存区。

##### 5.1、【git reset [ HEAD~数字] 文件名】

将指定版本的、指定的文件操作放在暂存区，将当前指定的文件从暂存区放回工作区。主要是`git reset HEAD 文件名`将指定文件从暂存区放回工作区

#### 6、【git reflog】

查看当前仓库版本改动的操作

#### 7、【git checkout -- 文件名】

从先从暂存区中拉取指定文件版本还原，如果没有暂存区中没有指定文件再到版本库中拉取还原（相当于清除指定文件在工作区的修改，包括删除文件后还原）。配合`git reset HEAD 文件名`，将指定文件添加到暂存区的修改放回工作区，然后`git checkeout -- 文件名`，可以删除已添加到暂存区的文件的修改。

注意： 只对已跟踪的文件有效

#### 8、【git rm 文件名】

相当于【`rm 文件名` + `git add 文件名`】或【`rm 文件名` + `git rm 文件名`】（直接git rm不香吗）的组合，会直接删除指定文件

注意： 只对已跟踪的文件有效

#### 9、【git remote 指令】

当先创建本地仓库，后创建远程仓库时，使用`git remote`将本地仓库和远程仓库关联，可以进行`push`/`pull`将本地仓库和远程仓库进行同步的操作

##### 9.1、【git remote add 远程仓库名 远程仓库url】

值远程仓库取仓库名（一般为origin），将远程仓库url和本地仓库关联。可以添加多个远程仓库（取不一样的远程仓库名就可以），本地仓库关联多个远程仓库，可以分别进行`push`/`pull`

##### 9.2、【git remote rm 远程仓库名】

删除本地仓库和指定远程仓库的关联（不会删除远程仓库，只是删除关联关系）

##### 9.3、【git remote set-url --add 远程仓库名 远程仓库url】

使用`git remote add 远程仓库名 远程仓库url`可以为本地仓库关联多个远程仓库，但是`push`只能推送给一个远程仓库名对应的远程仓库url。例如：每一个仓库名对应一个远程仓库url，我要给十个远程仓库推送，就要push十次。

使用【git remote set-url -add 远程仓库名 远程仓库url】可以给一个远程仓库名添加多个对应的url，`push`推送给一个远程仓库名对应的远程仓库url。例如：每一个仓库名对应十个远程仓库url，我要给十个远程仓库推送，只需要push一次。

注意：虽然一个远程仓库名能对应多个远程仓库url，能同时`push`到多个远程仓库，但是`pull`只会从第一个远程仓库url拉取

##### 9.4、【git remote set-url --delete 远程仓库名 远程仓库url】

删除指定远程仓库名的指定远程仓库url

##### 9.5、【git remote set-url 远程仓库名 旧的远程仓库url 新的远程仓库url】

修改指定远程仓库名的指定远程仓库url

##### 9.6、【git remote -v】

查看本地仓库和远程仓库的关联情况

#### 10、【git clone 远程仓库url】

当先创建远程仓库时，可以将远程仓库克隆到本地，这样直接就产生关联

#### 11、【git config [--global | --local] 配置名 配置值 】

为git设置一些配置，【--globe】表示这配置全局仓库都会使用，【--local】表示这配置只针对当前仓库。

例如：

// 添加配置

git config --global user.name "我的名字"

git config --global user.email "我的邮箱"

// 删除配置

git config --global --unset user.name 

git config --global --unset user.email

注意：user.name和user.email只是当前git用户的名字（用于表示推送人的名称）和邮箱（用于联系），不一定需要和远程仓库的用户名和邮箱一致（虽然一般来说都一样）

#### 12、【ssh-keygen -t rsa -C "备注"】

用于生成密钥（其实这不是git的指令），将公钥添加到远程仓库，便可以进行`push`操作

注意：【-C "备注"】其实是这个密钥的备注，一般来说都是远程仓库的邮箱

#### 13、【git checkout -b 分支名】

创建一条分支，并切换到分支上。相当于【`git branch 分支名`+`git checkout 分支名`】，使用`git branch`查看所有分支及当前HEAD所在的分支

#### 14、【git merge [--ff | --no-ff | --squash] -m "说明" 分支名】

用于将指定分支合并到当前分支上（不会删除指定分支）

合并分支时主要有三种合并模式：

`--ff` 也就是fast-forward（快进，默认的合并模式），如果顺着一个分支走下去可以到达另外一个分支的话，那么git在合并两者时，只会简单的把master的指针右移，此时可以不用写【-m "说明"】（写了也会忽略，也没有合并信息）。

优点：合并快，只需要把master指针右移就行

缺点：删除分支时，会丢失分支信息（合并后删除分支，看不出来合并过）；由于只是master指针移动，会把分支的提交记录合并到master分支，污染master分支

`--no-ff` 关闭fast-forward，合并时需要写【-m "说明"】，没有`--ff`的缺点

`--squash` 把一些不必要的commit进行压缩，例如：当前分支开发时commit很乱，在合并时不希望把这些历史commit带过来，于是使用`--squash`进行合并，此时文件已经同合并后一样了，但是不移动HEAD，不提交。需要进行一次额外的commit来"总结"一下，然后完成最终的合并。
