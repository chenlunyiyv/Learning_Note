# 一. 创建版本库

## 登陆自己的git账号

```bash
 git config --global user.name
 git config --global user.email "email@example.com"
```

## 创建一个版本库

```bash
mkdir Git_using
cd Git_using
pwd
```

>pwd命令用于显示当前目录。在我的Linux上，这个仓库位于Code/Learning_Note。

```bash
git init
```

>把这个目录变成Git可以管理的仓库

## 用命令git add告诉Git，把文件添加到仓库

>以readme.txt为例:

```bash
git add readme.txt
```

>执行上面的命令之后，没有任何显示,说明添加成功。  
>文件添加进去，实际上就是把文件修改添加到暂存区

## 用命令git commit告诉Git，把文件提交到仓库

>以刚刚提交的readme.txt为例:
>你可以在`git add readme.txt`加上如下代码

```bash
git commit -m 'my projest push'
```

__引号内的内容可以随便填写__
**,目的是描述记录每次上的内容是什么**
>简单解释一下`git commit`命令，-m后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。

# 二. 版本回退及其基本操作

## 版本控制系统命令可以告诉我们历史记录

```bash
git log
```

>`git log`命令显示从最近到最远的提交日志.如果嫌输出信息太多，看得眼花缭乱的，可以试试加上 --pretty=oneline 参数:

```bash
git log --pretty=oneline
```

## 版本回退

>回退到上一个版本

```bash
git reset --hard HEAD^
```

>不过且慢，然我们用git log再看看现在版本库的状态,发现我们已经找不到我们刚刚不想要的那个版本了,想再回去已经回不去了，肿么办？  
>
>办法其实还是有的，只要上面的命令行窗口还没有被关掉，你就可以顺着往上找啊找啊，找到那个分支版本号

```bash
git reset --hard 版本号
```

## 想要查查看指定文件的内容

```bash
 cat 文件名
```

## Git提供了一个命令用来记录你的每一次命令

```bash
git reflog
```

## 查看一下当前分支的状态

```bash
git status
```

<font color="#dd0000"  size="5">__强调:__</font>  
*第一次修改 -> `git add` -> 第二次修改 -> `git commit`*
>当你用`git add`命令后，在工作区的第一次修改被放入暂存区，准备提交，但是，在工作区的第二次修改并没有放入暂存区，所以，`git commit`只负责把暂存区的修改提交了，也就是第一次的修改被提交了，第二次的修改不会被提交。  
>
>那怎么提交第二次修改呢？你可以继续`git add`再`git commit`，也可以别着急提交第一次修改，先`git add`第二次修改，再`git commit`，就相当于把两次修改合并后一块提交了:

__必须:__
*第一次修改 -> git add -> 第二次修改 -> git add -> git commit*

## 丢弃工作区的修改

```bash
git checkout -- 文件名
```

>一种是让文件自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
>
>一种是让文件已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
>
>总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态。

## 删除文件

```bash
rm 文件名
git rm
```

>前者是将工作区中文件删除  
>后者从版本库中删除该文件

# 三. 添加远程库

## 添加远程库

>现在，我们根据GitHub的提示，在本地的lgit仓库下运行命令：

```bash
git remote add origin git@github.com:GitHub账户名
```

>添加后，远程库的名字就是origin，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库

## 下一步，就可以把本地库的所有内容推送到远程库上

```bash
git push -u origin master
```

>把本地库的内容推送到远程，用`git push`命令，实际上是把当前分支master推送到远程。  
>
>由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。

<font color="#00dd00"  size="5">__强调:__</font>
从现在起，只要本地作了提交，就可以通过命令：

```bash
git push -u origin master
```

## 从远程库克隆

```bash
git clone 地址
```

# 四. 分支管理

## 我们创建dev分支，然后切换到dev分支

```bash
git checkout -b dev
```

>`git checkout`命令加上-b参数表示创建并切换，相当于以下两条命令：

```bash
git branch dev
git checkout dev
```

## 查看当前分支

```bash
git branch
```

>`git branch`命令会列出所有分支，当前分支前面会标一个*号。
>  
>如果dev分支的工作完成，我们可以切换回master分支：

```bash
git checkout master
```

## 把分支的工作成果合并到master分支上

```bash
git merge 分支名
```

>git merge命令用于合并指定分支到当前分支。

## 合并完成后，就可以放心地删除分支了

```bash
git branch -d 分支名
```

## 创建并切换到新的分支，可以使用

```bash
git switch -c 分支名
```

>我们注意到切换分支使用`git checkout 分支名`，而前面讲过的撤销修改则是`git checkout -- 文件名`，同一个命令，有两种作用，确实有点令人迷惑。所以才出现这种switch命令.

## 直接切换到已有的master分支，可以使用

```bash
git switch master
```

## 解决冲突

>出现冲突,Git告诉我们，某些文件存在冲突，必须手动解决冲突后再提交。`git status`也可以告诉我们冲突的文件：

```bash
git status
```

>查看的冲突文件的内容  
>  
>`cat 文件名`  
>Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容

## 用带参数的`git log`也可以看到分支的合并情况

```bash
git log --graph --pretty=oneline --abbrev-commit
```

## 分支管理策略

```bash
git merge --no-ff -m "merge with no-ff" dev
```

>合并分支，注意--no-ff参数，表示禁用Fast forward  
>
>因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去

## 两个工作同时进行

>第一个工作只进行到一半，还没法提交。但是，必须在一定时间内修复该bug(进行另一个工作)，怎么办？
>  
>Git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作：

```bash
git stash
```

>将BUG修复后合并,删除BUG分支,然后切换到第一个工作区`git checkout 分支名`,但是工作区是干净的，刚才的工作现场存到哪去了？用`git stash list`命令看看  
>
>工作现场还在，Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：
>  
>一是用`git stash apply`恢复，但是恢复后，stash内容并不删除，你需要用`git stash drop`来删除；
>  
>另一种方式是用`git stash pop`，恢复的同时把stash内容也删了
>  
>再用git stash list查看，就看不到任何stash内容了

```bash
#查看工作区
git stash list
#恢复工作区并删除stash
git stash apply
git stash drop
#恢复工作区的同时删除stash
git stash pop
```

## 强行删除分支

```bash
git branch -D 分支名
```

>如果要丢弃一个没有被合并过的分支，可以通过`git branch -D <name>`强行删除

## 要查看远程库的信息

```bash
git remote
#or
git remote -v
```

>查看远程库的信息，要用`git remote`,用`git remote -v`显示更详细的信息

## 推送分支

```bash
#推送主分支
git push origin master
#推送其他分支
git push origin 分支名
```

## 抓取分支(多人开发)

>现在，别人要在dev分支上开发，就必须创建远程origin的dev分支到本地，于是他用这个命令创建本地dev分支：

```bash
git checkout -b dev origin/dev

git push origin dev
```

>别人已经向origin/dev分支推送了他的提交，而碰巧你也对同样的文件作了修改，并试图推送
>  
>推送失败，因为别人的最新提交和你试图推送的提交有冲突，解决办法也很简单，Git已经提示我们，先用`git pull`把最新的提交从origin/dev抓下来，然后，在本地合并，解决冲突，再推送

```bash
git push
```

>然而，git pull也失败了，原因是没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接

```bash
git branch --set-upstream-to=origin/dev dev
git pull
```

>这回`git pull`成功，但是合并有冲突，需要手动解决，解决的方法和分支管理中的**解决冲突**完全一样。解决后，提交，再`push`

```bash
git commit -m "fix env conflict"
git push origin dev
```

>因此，多人协作的工作模式通常是这样:
>  
>&ensp;&ensp;1.首先，可以试图用`git push origin <branch-name>`推送自己的修改；
>  
>&ensp;&ensp;2.如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
>  
>&ensp;&ensp;3.如果合并有冲突，则解决冲突，并在本地提交；
>  
>&ensp;&ensp;4.没有冲突或者解决掉冲突后，再用`git push origin <branch-name>`推送就能成功！
>  
>如果`git pull`提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`。

这就是多人协作的工作模式，一旦熟悉了，就非常简单。

## rebase操作

>rebase操作可以把本地未push的分叉提交历史整理成直线；  
>
>在上一节我们看到了，多人在同一个分支上协作时，很容易出现冲突。即使没有冲突，后push(推送提交)的童鞋不得不先pull(拉取网上代码)，在本地合并，然后才能push成功

```bash
git pull
git status
git log --graph --pretty=oneline --abbrev-commit
git rebase
git log --graph --pretty=oneline --abbrev-commit
git push origin master
git log --graph --pretty=oneline --abbrev-commit
```

>先pull一下，看看我们与其他分支的区别，再用`git status`看看状态；加上刚才合并的提交，用`git log`看看情况。输入rebase，输出了一大堆操作，到底是啥效果？再用`git log`看看。rebase操作的特点：把分叉的提交历史“整理”成一条直线，看上去更直观。缺点是本地的分叉提交已经被修改过了。最后，通过push操作把本地分支推送到远程。再用git log看看效果，远程分支的提交历史也是一条直线。

# 五. 标签管理

## 创建标签

>敲命令`git tag <name>`就可以打一个新标签

```bash
git tag v1.0
```

>可以用命令git tag查看所有标签：

```bash
git tag
```

><font color="#0000dd"  size="5">注意:</font>标签不是按时间顺序列出，而是按字母排序的。可以用`git show <tagname>`查看标签信息：

```bash
git show v1.0
```

>还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字：

```bash
git tag -a v0.1 -m "version 0.1 released" 1094adb
```

>用命令`git show <tagname>`可以看到说明文字：

```bash
git show v0.1
```

## 操作标签

>如果标签打错了，也可以删除：

```bash
git tag -d v0.1
```

>因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。
>  
>如果要推送某个标签到远程，使用命令`git push origin <tagname>：`

```bash
git push origin v1.0
```

>或者，一次性推送全部尚未推送到远程的本地标签：

```bash
git push origin --tags
```

>如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除：

```bash
git tag -d v0.9
```

>然后，从远程删除。删除命令也是push，但是格式如下：

```bash
git push origin :refs/tags/v0.9
```

# 六. 自定义Git

>让Git显示颜色，会让命令输出看起来更醒目：

```bash
git config --global color.ui true
```

## 忽略特殊文件

>在Git工作区的根目录下创建一个特殊的.gitignore文件，然后把要忽略的文件名填进去，Git就会自动忽略这些文件。不需要从头写.gitignore文件，GitHub已经为我们准备了各种配置文件，只需要组合一下就可以使用了。所有配置文件可以直接在线浏览：`https://github.com/github/gitignore`

>忽略文件的原则是：  
>&ensp;&ensp;忽略操作系统自动生成的文件，比如缩略图等；  
>&ensp;&ensp;忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库;  
>&ensp;&ensp;比如Java编译产生的.class文件；  
>&ensp;&ensp;忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。
>  
>有些时候，你想添加一个文件到Git，但发现添加不了，原因是这个文件被.gitignore忽略了：

```bash
git add App.class
```

>如果你确实想添加该文件，可以用-f强制添加到Git：

```bash
git add -f App.class
```

>或者你发现，可能是.gitignore写得有问题，需要找出来到底哪个规则写错了，可以用git check-ignore命令检查：

```bash
git check-ignore -v App.class
```

## 配置别名

>有没有经常敲错命令？比如git status？status这个单词真心不好记。如果敲git st就表示git status那就简单多了，当然这种偷懒的办法我们是极力赞成的。我们只需要敲一行命令，告诉Git，以后st就表示status：


```bash
git config --global alias.st status
```

>当然还有别的命令可以简写，很多人都用co表示checkout，ci表示commit，br表示branch：

```bash
git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.br branch
```

>以后提交就可以简写成：

```bash
git ci -m "bala bala bala..."
```

>--global参数是全局参数，也就是这些命令在这台电脑的所有Git仓库下都有用。
>  
>命令`git reset HEAD file`可以把暂存区的修改撤销掉（unstage），重新放回工作区。既然是一个unstage操作，就可以配置一个unstage别名：

```bash
git config --global alias.unstage 'reset HEAD'
```

>当你敲入命令：

```bash
git unstage test.py
```

>实际上Git执行的是：

```bash
git reset HEAD test.py
```

>配置一个git last，让其显示最后一次提交信息：

```bash
git config --global alias.last 'log -1'
```

>这样，用git last就能显示最近一次的提交

```bash
git last
```

>配置Git的时候，加上--global是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用.配置文件放哪了？每个仓库的Git配置文件都放在.git/config文件中：

```bash
cat .git/config
```

>别名就在[alias]后面，要删除别名，直接把对应的行删掉即可。而当前用户的Git配置文件放在用户主目录下的一个隐藏文件.gitconfig中：

```bash
cat .gitconfig
```

>配置别名也可以直接修改这个文件，如果改错了，可以删掉文件重新通过命令配置。

## 搭建Git服务器

>**&ensp;&ensp;&ensp;&ensp;GitHub就是一个免费托管开源代码的远程仓库。但是对于某些视源代码如生命的商业公司来说，既不想公开源代码，又舍不得给GitHub交保护费，那就只能自己搭建一台Git服务器作为私有仓库使用。**
>  
>**&ensp;&ensp;&ensp;&ensp;搭建Git服务器需要准备一台运行Linux的机器，强烈推荐用Ubuntu或Debian，这样，通过几条简单的apt命令就可以完成安装。假设你已经有sudo权限的用户账号，下面，正式开始安装。**

>第一步，安装git：

```bash
sudo apt-get install git
```

>第二步，创建一个git用户，用来运行git服务：

```bash
sudo adduser git
```

>第三步，创建证书登录：
>  
>&ensp;&ensp;&ensp;&ensp;收集所有需要登录的用户的公钥，就是他们自己的id_rsa.pub文件，把所有公钥导入到/home/git/.ssh/authorized_keys文件里，一行一个。
>  
>第四步，初始化Git仓库：

>先选定一个目录作为Git仓库，假定是/srv/sample.git，在/srv目录下输入命令：

```bash
sudo git init --bare sample.git
```

>Git就会创建一个裸仓库，裸仓库没有工作区，因为服务器上的Git仓库纯粹是为了共享，所以不让用户直接登录到服务器上去改工作区，并且服务器上的Git仓库通常都以.git结尾。然后，把owner改为git：

```bash
sudo chown -R git:git sample.git
```

>第五步，禁用shell登录：
>  
>&ensp;&ensp;&ensp;&ensp;出于安全考虑，第二步创建的git用户不允许登录shell，这可以通过编辑/etc/passwd文件完成。找到类似下面的一行：

```bash
git:x:1001:1001:,,,:/home/git:/bin/bash
```

>改为：

```bash
git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell

```

>这样，git用户可以正常通过ssh使用git，但无法登录shell，因为我们为git用户指定的git-shell每次一登录就自动退出。

>第六步，克隆远程仓库：
>  
>&ensp;&ensp;&ensp;&ensp;现在，可以通过git clone命令克隆远程仓库了，在各自的电脑上运行：

```bash
git clone git@server:/srv/sample.git
```

>剩下的推送就简单了。

### 管理公钥

>>如果团队很小，把每个人的公钥收集起来放到服务器的/home/git/.ssh/authorized_keys文件里就是可行的。如果团队有几百号人，就没法这么玩了，这时，可以用Gitosis来管理公钥。
>>  
>>这里我们不介绍怎么玩Gitosis了，几百号人的团队基本都在500强了，相信找个高水平的Linux管理员问题不大。

### 管理权限

>>有很多不但视源代码如生命，而且视员工为窃贼的公司，会在版本控制系统里设置一套完善的权限控制，每个人是否有读写权限会精确到每个分支甚至每个目录下。因为Git是为Linux源代码托管而开发的，所以Git也继承了开源社区的精神，不支持权限控制。不过，因为Git支持钩子（hook），所以，可以在服务器端编写一系列脚本来控制提交等操作，达到权限控制的目的。Gitolite就是这个工具。

参考https://www.liaoxuefeng.com/wiki/896043488029600