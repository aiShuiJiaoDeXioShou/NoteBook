# git的常用命令

**创建仓库**

~~~less
git init 文件夹所在的路径
~~~

**复制其指定仓库**

~~~less
git clone 仓库地址
~~~

**创建用户名以及邮箱名称**

~~~less
$ git config --global user.name "runoob"
$ git config --global user.email test@runoob.com
~~~

**提交代码操作**

~~~less
$ git add *.c
$ git add README
$ git commit -m '初始化项目版本'
~~~

**创建远端的别名，`origin`就是别名，后面接的是远端的链接**

~~~less
$ git remote add origin git@github.com:tianqixin/runoob-git-test.git
~~~

**获取所有远端名称**

~~~less
git remote -v
~~~

**提交到该远端`master`分支**

~~~less
$ git push -u origin master
~~~

**刷新数据，合并指定代码**

~~~less
$ git pull
~~~

# git-study

**常用操作文件的命令**

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20211201174648047.png" alt="image-20211201174648047" style="zoom:200%;" />

**linux下常用的操作文件的命令**

~~~less
cd 目录 --打开一个目录
cd.. 退回上一级目录
pwd 显示当前所在的目录路径
ls 显示当前目录所有的文件
lsll 详细的显示当前目录所有的文件
mkdir 新建一个文件夹
rm -r 删除一个文件夹
rm -r / 删除一切文件夹
reset 重新初始化终端
clear 清屏
help 帮助 
exit 退出
#表示注解
~~~

~~~less
//--global 这个英文名称的全球的意思 git 里面用于设置密码 用户名 邮箱
git config --global
~~~

git配置本身就是储存在文件里面的,这个是我自己的文件地址:

~~~less
C:\Users\有天道\.gitconfig
~~~

![image-20211201182254514](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20211201182254514.png)

**git的基本命令操作**

![image-20211201182755977](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20211201182755977.png)



对分支进行管理：

> 蒋磊 19:06:29
> 1.创建分支：$ git branch jiang
>
> 2.切换分支： $ git checkout jiang
>
> 3.$ git add .
>
> 4.$ git remote add jiang 
> ![img](file:///D:\Tencent Files\2832294398\Image\Group2\[R\)(\[R)(F8H3IKU(@43DQ[32YWO.png)
> ![img](file:///C:\Users\有天道\AppData\Roaming\Tencent\QQTempSys\8LDO48C$8@[GWU0353$FOVS.png)https://gitee.com/lwlspace/eshop-backend-java.git（git仓库地址）
>
> 5.$ git commit -m "jiang's first" .
>
> 6.$ git push jiang jiang
> 1.创建分支：$GIT支行江
>
> 2.切换分支：$git结帐江
>
> 3.加$git。
>
> 4.$Git遥控器
> ![img](file:///D:\Tencent Files\2832294398\Image\Group2\[R\)(\[R)(F8H3IKU(@43DQ[32YWO.png)
> ![img](file:///C:\Users\有天道\AppData\Roaming\Tencent\QQTempSys\8LDO48C$8@[GWU0353$FOVS.png)Https://gitee.com/lwlspace/eshop-backend-java.git(git仓库地址)
>
> 5.$GIT承诺-“江第一”。
>
> 6.$git推动江
>
>
> 蒋磊 19:06:45
> $ git clone -b teamv1 
> ![img](file:///D:\Tencent Files\2832294398\Image\Group2\[R\)(\[R)(F8H3IKU(@43DQ[32YWO.png)
> ![img](file:///C:\Users\有天道\AppData\Roaming\Tencent\QQTempSys\8LDO48C$8@[GWU0353$FOVS.png)https://gitee.com/lwlspace/eshopAppVue.git
>
> git clone -b 分支名 仓库地址
>
> 蒋磊 19:06:57
> git克隆指定分支代码

创建分支:

> git branch yang

切换分支:

> git checkout yang

提交到该分支

>  git push -u origin yang

合并该分支:

> git merge wang

提交到该分支:

> git commit -m "提交信息"

push一下

> git push -u origin 分支名称





合并分支:

> # [git命令合并分支代码](https://www.cnblogs.com/linjiqin/p/7756164.html)
>
> 对于复杂的系统，我们可能要开好几个分支来开发，那么怎样使用git合并分支呢？
>
> 合并步骤：
> 1、进入要合并的分支（如开发分支合并到master，则进入master目录）
> git checkout master
> git pull
>
> 2、查看所有分支是否都pull下来了
> git branch -a
>
> 3、使用merge合并开发分支
> git merge 分支名
>
> 4、查看合并之后的状态
> git status
>
> 5、有冲突的话，通过IDE解决冲突；
>
> 6、解决冲突之后，将冲突文件提交暂存区
> git add 冲突文件
>
> 7、提交merge之后的结果
> git commit
>
> 如果不是使用git commit -m "备注" ，那么git会自动将合并的结果作为备注，提交本地仓库；
>
> 8、本地仓库代码提交远程仓库
> git push
>
> git将分支合并到分支，将master合并到分支的操作步骤是一样的。
