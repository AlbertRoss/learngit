* <b>git init</b> -初始化一个Git仓库，初始完会产生一个.git文件，默认看不到，想要查看，可以输入命令<b>ls -ah</b>来查看
* <b>git add readme.txt</b>  -表示暂存所有新增的readme.txt文件，可以空格分开添加多个文件，实际上就是把文件修改添加到暂存区；
* <b>git add .</b>    -表示暂存所有新增文件，实际上就是把文件修改添加到暂存区；
* <b>git commit -m "描述文字"</b> -提交文本并填写描述信息，提交更改，实际上就是把暂存区的所有内容提交到当前分支。
* <b>git log</b> -查看提交历史，命令显示从最近到最远的提交日志，如果嫌输出信息太多，可以加上--pretty=oneline参数：即<b>git log --pretty=oneline</b>，可以看到GIT的commit的id和commit是的文本信息
* <b>git relog</b> -查看命令历史，命令显示从最近到最远的命令历史提交记录
* <b>git reset --hard "版本信息"</b> -表示git回退的版本。在Git中，用<b>HEAD</b>表示当前版本，也就是最新的提交6c1f14f0a...（注意我的提交ID和你的肯定不一样），上一个版本就是<b>HEAD^</b>，上上一个版本就是<b>HEAD^^</b>，当然往上100个版本写100个^比较容易数不过来，所以写成<b>HEAD~100</b>。举例如下：
  * git reset --hard HEAD^  -回退到上一个版本
  * git reset --hard HEAD^^ 等同于git reset --hard HEAD2 -回退到上上一个版本
  * git reset --hard 6c1f1  -表示hard + commit的id号（至少4位），根据id号回退到指定版本
* <b>git status</b> -查看当前工作状态

<b>场景案例</b>：如果修改的readme.txt之后，执行`git add readme.txt`，再修改readme.txt再执行`git commit -m 'git tracks changes' `，用`git status`查看发现只有第一个修改的提交了，第二次修改的没有提交，只是因为只要增加到了缓存区（执行了git add）才可以被提交。解决方法：你可以继续`git add`再`git commit`，也可以别着急提交第一次修改，先`git add`第二次修改，再`git commit`，就相当于把两次修改合并后一块提交了：

第一次修改 -> `git add` -> 第二次修改 -> `git add` -> `git commit`

* <b>git checkout -- 文件名</b>  -如`git checkout -- readme.txt`把`readme.txt`文件在工作区的修改全部撤销，这里有两种情况：

  一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

  一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

  总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态。

<b>撤销修改场景</b>

<b>场景1：</b>当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。

<b>场景2：</b>当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD `，就回到了场景1，第二步按场景1操作。

<b>删除文件的场景</b>

<b>场景1：</b>确实要从版本库中删除文件，用命令`git rm 文件名`,并且`git commit -m '说明'`即可。

<b>场景2：</b>删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本：用`git checkout -- 文件名`，其实就是用版本库里的版本替换工作区的版本

<b>本地创建SSH Key</b>

为了连接远程仓库，第一步：需要本地创建SSH Key，在根目录中输入

 `ssh-keygen -t rsa -C "email地址"`

一路回车，使用默认值即可。可以在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。第二步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容：

<b>添加远程库</b>

要关联一个远程库，使用命令

`git remote add origin git@github.com:AlbertRoss/learngit.git`

关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；

此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改即可；

<b>从远程克隆</b>

`git clone 项目的ssh地址` 克隆到本地，Git支持多种协议，包括`https`，但`ssh`协议速度最快。

`cd 项目文件夹名字` 进入项目

`ls` 查看项目中全部文件

<h5>创建与合并分支</h5>

* <b>git branch</b> -查看所有分支

* <b>git branch <name></b>  -创建名字为name的分支

* <b>git switch <name> 或者 git checkout <name> </b> -切换到name分支，使用switch更科学

* <b>git switch -c <name> 或者 git checkout -b <name> </b> -创建+切换分支

* <b>git merge <name></b> -合并某分支到当前分支

* <b>git branch -d <name></b> -删除分支

  合并分支时注意：上面的`Fast-forward`信息，Git告诉我们，这次合并是“快进模式”，也就是直接把`master`指向`dev`的当前提交，所以合并速度非常快。当然，也不是每次合并都能`Fast-forward`。

<h5>解决冲突问题</h5>

在feature1分支上提交 Creating a new branch is quick AND simple.

在master分支上提交Creating a new branch is quick & simple.

 可以使用<b>git status</b>查看冲突的问题，然后打开文件进行修改，Git用`<<<<<<<`，`=======`，`>>>>>>>`标记出不同分支的内容，<<<和===之间的为当前更改的内容，===和>>>之间的内容为分支中更改的内容，删除这样标签，然后剩下最终要提交的内容，如‘Creating a new branch is quick and simple.’，确定好内容了再执行提交：git add readme.txt     git commit -m 'conflict fixed' 即可。

可以使用带参数的<b>git log</b>查看分支合并情况

* <b>git log --graph --pretty=oneline --abbrev-commit</b> -查看分支提交记录，带hash码和commit文本。
* <b>git log --graph</b> -可以看到分支合并图。

<h5>分支管理策略</h5>

Git会用`Fast forward`模式，但这种模式下，删除分支后，会丢掉分支信息。

如果要强制禁用`Fast forward`模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。