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

url:https://www.liaoxuefeng.com/wiki/896043488029600/897271968352576
git add .
git commit -m 'update Note.md'