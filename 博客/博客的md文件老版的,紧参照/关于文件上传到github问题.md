---
layout: =
title: '关于文件上传到github问题 '
date: 2018-09-02 11:05:21
tags:
    - 学习
    - github
---

<!-- more -->

# 关于文件上传到github的操作
## 步骤如下

1. 在要上传的文件夹下打开GitBash
2. 输入以下命令（用户和邮箱为你github注册的账号和邮箱）
```
$ git config --global user.name "用户名"
$ git config --global user.email "注册时的邮箱"
```
3. 密钥的生成（如果有此步骤省略）
```
$ ssh-keygen -t rsa -C "邮箱"
```
生成，生成过程中一路按3次回车键就好了。（默认路径，默认没有密码登录）
生成成功后，去对应目录C:\Users\bo.ssh里（bo为电脑用户名，每个人不同）用记事本打开id_rsa.pub，得到ssh key公钥。
然后在github上新建SSH钥匙复制id_rsa.pub到上面去就行
4. 本地上传
执行指令：git init
5. 将所有文件添加到仓库
``` 
  git add .
```
6. 将某个文件添加到仓库
```
git add **.cpp    //添加当前文件夹下的**.cpp这个文件
```
7. 对文件进行文件注释
```
   $ git commit -m "注释内容"  //引号中的内容为对该文件的描述
```
8. 将内容复制到仓库中
```
$ git remote add origin 加密钥（或者https:)
$ git remote add origin git@github.com:xfbxfbxfb/picture.git    
$ git remote add origin https://github.com/xfbxfbxfb/picture.git
```
**注意:**
如果出现错误：fatal: remote origin already exists，则执行以下语句：
```
$ git remote rm origin 
$ git remote add origin 加密钥（或者https:)
```
9. 最后执行
```
  $ git push origin master
```
如果出现错误failed to push som refs to…….，则执行以下语句，先把远程服务器github上面的文件拉先来，再push 上去。：
```
 $ git pull origin master
 ```
 10. 删除某个文件
首先进入你的master文件夹下, Git Bash Here ,打开命令窗口
$ git --help                                      # 帮助命令
$ git pull origin master                    # 将远程仓库里面的项目拉下来
$ dir                                                # 查看有哪些文件夹
$ git rm -r --cached target              # 删除target文件夹
$ git commit -m '删除了target'        # 提交,添加操作说明
$ git push -u origin master               # 将本次更改更新到github项目上去
