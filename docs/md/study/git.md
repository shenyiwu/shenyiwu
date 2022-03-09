# Git基本命令

1.查看已配置的信息

```
git config --global --list
```

2.打开git bash工具配置git的user name和email，用于身份验证，依次输入：

```
git config --global user.name "your name"
git config --global user.email "your email"
```

3.执行以下语句来判断是否已经存在本地公钥

```
cat ~/.ssh/id_rsa.pub
```

4.生成公钥ssh key

```
ssh-keygen -t rsa -C "shenjianhong"
```

5.获取生成的公钥

```
cat ~/.ssh/id_rsa.pub
```

下载项目的最新更改，用于拉取某分支的最新副本（建议工作时每次都输入这个命令）(远端: origin) (分支名称: 可以是"master"或者是一个已经存在的分支)。

```
git pull 远端 分支名称 -u
```

pull出现refusing to merge unrelated histories，可以在pull命令后紧接着使用`--allow-unrelated-history`选项来解决问题（该选项可以合并两个独立启动仓库的历史）

浏览您所做的更改

```
git status
```

将更改加入到本次提交

当输入"git status"时，您的更改会显示为红色。

```
git add 红色的修改
git commit -m "提交的描述"
```

提交您的更改到服务器

```
git push 远端 分支名称
```

删除代码库的所有更改（包含未跟踪的文件）

```
git clean -f
```

将某分支合并到master分支

```
git merge 分支名称
```

克隆远程仓库到本地指定目录

```
git clone https://gitee.com/shenyiwu/test.git ./
```

添加本地文件

```
git add a.text
git commit -m "a text commit"
```



```
1.克隆飞进远程仓库到本地
git clone git@gitlab.51feijin.com:develop/crystalErp.git ./

2.获取远程origin/master分支与当前分支合并
git pull origin master

3.将本地的 master 分支推送到 origin 主机的 master 分支
git push origin master
```

获取当前机器RSA秘钥：ssh-keygen -t rsa -C "shengjianhong"

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDotqi5brCVFRCQIlVMI8UpZjkuPp2UkL6C+NUEl4mTEyyKo+ow0h8ZSXcDW+Tb0VS/uEejtnDP/MZwfOHYkRqJ89n6b0ORWcGMm4IlMrVXCd1yp8knzQQg7dEZ/e5PyYf3cSDHZoW+25ZhFJiHUDlz4E8whFQo00Jp51ZVN4EA+mjJcQSUkMcTHjBd/Bt43IH8ggmIG/aQGNvLVJOMuA6a8t+WGNDol2uUcP/dYN8hDA41lGzGDA6/9uGLkbXUcA4W33ErQMvrYA0WsWC3vdLv65R229i1RErh/gN7t0YZdHzc7b9Sof46D8+g1a0/1sDr7tJL+teY7iQXGcr2w7KfDZ4mFaiK9+OHtOrVnvaXFJbw4QP2i8V1Tk1L7EjoDwXEiVZH2jygiq+57tnsHNvGm4xkkb1WijC3tprBxdgYIZ0KKyCdaS51N13OZ3JFGy+L6r81oqcQnXspRqSHvaTw7+o2t1fKE/VnJacGJVZDK90liL5V1e8qNHIOfshzeL0= Administrator@SC-201907291447
```



端口映射

```
https://natapp.cn/tunnel/lists

shenjianhong
```