##  搭建步骤：
一 安装git

$ sudo apt-get install git

查看git版本

$ git version

二 安装Node.js及npm

1.可以直接命令安装,但是命令安装的不是最新版本。

    $ sudo apt-get install nodejs
    $ sudo apt-get install npm


2 本博客采用第二种方法，首先官网下载最新版，然后解压。将node,npm命令设置全局命令：

    $ sudo ln -s /home/dudefu/Documents/node-v8.6.0-linux-x64/bin/node /usr/local/bin/node
    $ sudo ln -s /home/dudefu/Documents/node-v8.6.0-linux-x64/bin/npm /usr/local/bin/npm



查看版本：

    $ node -v
    $ npm -v

3、 安装hexo

$ npm install -g hexo-cli

hexo-cli安装路径/home/dudefu/Documents/node-v8.6.0-linux-x64/lib/node_modules/hexo-cli，此时输入命令hexo会提示“未找到命令”，此时要将hexo-cli/bin/文件夹下的hexo命令设置为全局：

     $ sudo ln -s /home/dudefu/Documents/node-v8.6.0-linux-x64/lib/node_modules/hexo-cli/bin/
    $ hexo /usr/local/bin/hexo

再输入hexo命令可以正常显示。 
 
创建一个空文件夹，此处名为hexo：

    $ mkdir hexo
    $ cd hexo
    $ hexo init .
    $ npm install 
    $ hexo server -p 5000

到此，hexo安装完毕。浏览器输入本地，前面配置均正确的情况下，正常显示博客首页。 
4、 hexo配置 
主要分为两块站点配置和主题配置。此处先下载NexT主题：

$ git clone https://github.com/iissnan/hexo-theme-next themes/next
1
接下来的详细配置就不细说了，直接看hexo文档，NexT使用文档，主题配置遇到难点的可以访问github：，所有的问题基本可以解决。

我的博客
--------------------- 
作者：夜下探戈 
来源：CSDN 
原文：https://blog.csdn.net/dudefu011/article/details/78124146 
版权声明：本文为博主原创文章，转载请附上博文链接！