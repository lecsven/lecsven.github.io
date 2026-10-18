
---
title: 用Github Pages 发表文章
date: 2020-12-25 16:30:49



---

现在有很多免费的发表文章的平台，比如简书、公众号、知乎等等，但是这些网站对发表的文章会有比较严格的审核，有时候会审核不通过，但是并不告诉你原因。

就算能通过了，多一个平台发表就相当于多了一个备份，所以我就想寻找一个免费但是比较靠谱而且比较自由的发布平台。Github Pages就是这样的平台。

用**Hexo**框架，可以使用**Markdown**来写文章，然后上传到**github**上面，网页就会自动更新了。

下面简单记录下流程，当作备忘。

首先安装node.js，安装npm，安装git ，具体教程网上很多，这里就不赘述了。

以下命令可以查看版本：

![image-20201225105608896](/images/github-pages-post/01.png)

注册Github 账号，然后新建New repository:

![image-20201225105642727](/images/github-pages-post/02.png)

名字以`github.io`结尾

![image-20201225105807410](/images/github-pages-post/03.png)

创建完：



![image-20201225110029160](/images/github-pages-post/04.png)



设置主题：





![image-20201225110614663](/images/github-pages-post/05.png)





![image-20201225110809768](/images/github-pages-post/06.png)



选择一个喜欢的主题：



![image-20201225122439852](/images/github-pages-post/07.png)



打开网页如此显示：



![image-20201225134340815](/images/github-pages-post/08.png)

## 安装hexo



我在电脑上面新建一个文件夹**blog**，路径在：H:\Dropbox\blog

右键Git bash here，打开git窗口

输入`npm i hexo-cli -g`安装Hexo

![image-20201225122832550](/images/github-pages-post/09.png)

`hexo -v`查看hexo是否安装成功

![image-20201225122856499](/images/github-pages-post/10.png)

输入`hexo init`初始化文件夹

![image-20201225122929375](/images/github-pages-post/11.png)

`npm install`安装必备的组件

![image-20201225122950017](/images/github-pages-post/12.png)



添加自己的文章到H:\Dropbox\blog\source\_posts路径下面：

在H:\Dropbox\blog\source\_posts下面是这样的：

![image-20201225123318427](/images/github-pages-post/13.png)



`hexo g`生成静态网页

![image-20201225123036565](/images/github-pages-post/14.png)

`hexo s`打开本地服务器

![image-20201225123056279](/images/github-pages-post/15.png)



刷新一下http://localhost:4000/页面：

把我们自己的文章显示在页面上了。

![image-20201225123354344](/images/github-pages-post/16.png)

接下来就把文章上传到github上面

按`ctrl+c`关闭本地服务器。

设置Github的`user.name`和`user.email`，这个是必须的。

![image-20201225125017698](/images/github-pages-post/17.png)

生成密钥SSH key：

![image-20201225124939610](/images/github-pages-post/18.png)

获取密钥：

![image-20201225125548986](/images/github-pages-post/19.png)

可以在本地查看到这个密钥：

![image-20201225124840290](/images/github-pages-post/20.png)

打开后这样显示：

与上面的显示的密钥是一样的。

![image-20201225125107397](/images/github-pages-post/21.png)

打开github.com，选择`Setting` 

![image-20201228174208392](/images/github-pages-post/22.png)

左边选择`SSH and GPG keys` ，然后右上角选择`New SSH key`

![image-20201228174436585](/images/github-pages-post/23.png)

新建一个SSH keys，名字随便。

![image-20201225125220715](/images/github-pages-post/24.png)

创建完了：

![image-20201225125349110](/images/github-pages-post/25.png)



测试一下，输入`ssh -T git@github.com`

![image-20201225125754236](/images/github-pages-post/26.png)

成功了。

`_config.yml`文件最后一行：

```markdown
deploy:
  type: git
  repository: https://github.com/lecsven/practice.github.io
  branch: master
```

repository修改为你自己的github项目地址。



![image-20201225130823965](/images/github-pages-post/27.png)

![image-20201225131029315](/images/github-pages-post/28.png)



会发现H:\Dropbox\blog\source\_posts多了个文件：new-article.md

在文件里面修改好文字。

然后`hexo g`生成静态网页，`hexo s`可以本地预览效果：

![image-20201225131306647](/images/github-pages-post/29.png)

最后输入`hexo d`上传到github上，会需要输入用户名和密码，密码可能是弹出的窗口。

![image-20201225131820271](/images/github-pages-post/30.png)

好了，能够在网页上看到更新后的文章了。



![image-20201228180051775](/images/github-pages-post/31.png)



这是一个比较不错的文章备份仓库。可以自由修改，更改主题，不断折腾新的功能。还有很多新的功能下次继续聊。

