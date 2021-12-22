#### 1、【git init】

初始化git仓库

#### 2、【git add 文件名】

将文件添加到暂存区

#### 3、【git commit -m "提交说明"】

将暂存区文件添加提交到git仓库进行版本管理

#### 4、【git log [--oneline] [--graph]】

查看提交的版本，`--oneline`相当于`--pretty=oneline --abbrev-commit`，表示输出格式为一行并且只展示版本的前几位

#### 5、【git reset [--hard | -- mixed | soft] [ HEAD~数字 | 版本号 ]】

`HEAD~数字` 数字表示回到前几个版本（若只写`HEAD`表示回到当前版本，可以用于重置工作区、暂存区文件），或者回到指定版本，除了未被跟踪的文件不会受影响，其他参数对文件影响如下：

`
--hard `【删除】指定版本中已commit文件在工作区和暂存区的修改、指定版本之后的所有文件；

`
--mixed` 【保存】指定版本中已commit文件在工作区和暂存区的修改、指定版本之后的所有文件。指定版本中已commit文件在工作区和暂存区的修改都放回工作区，指定版本之后的所有文件变成未被跟踪的文件放在工作区；

`
--soft` 【保存】指定版本中已commit文件在工作区和暂存区的修改、指定版本之后的所有文件。在工作区和暂存区的修改仍在工作区和暂存区，指定版本之后的所有commit文件变成未被跟踪的文件放在暂存区

