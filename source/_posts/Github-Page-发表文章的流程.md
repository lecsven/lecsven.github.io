---
title: Github Page 发表文章的流程
date: 2021-05-06 11:31:28
tags:
---



找到blog本地的文件夹，我的目录`H:\Dropbox\all-blog\lecsven.github.io\`

右键选择”Git Bash Here"

![image-20210506112733590](/images/github-pages-flow/01.png)



输入`hexo new post "文章名字"`，注意文章名的双引号得确认是英文输入的。

![image-20210506113308742](/images/github-pages-flow/02.png)

然后在`H:\Dropbox\all-blog\lecsven.github.io\source\_posts\`打开md文件

![image-20210506113837848](/images/github-pages-flow/03.png)

开始写文章

![image-20210506114034412](/images/github-pages-flow/04.png)

完成之后按照以下顺序操作：

```powershell
git status # 查看 git 仓库的变化
git add . # 添加全部修改到寄存区
git commit -m 'changed' # 提交
git push origin hexo # 推送到远程仓库的 hexo 分支
```

操作完成：

![image-20210506114346103](/images/github-pages-flow/05.png)

打开`https://github.com/lecsven/lecsven.github.io`查看状态

![image-20210506114555327](/images/github-pages-flow/06.png)

确认静态文件已经正确上传：

![image-20210506114652456](/images/github-pages-flow/07.webp)

**接下来部署静态文件，使得内容可以在网页上面正常显示**



在`H:\Dropbox\all-blog\lecsven.github.io`文件夹下面的`_config.yml`里面

确保如下设置：

```yaml
deploy:
  type: git
  repository: https://github.com/lecsven/lecsven.github.io.git
  branch: master
```

`  branch: master`能够让部署的文件直接上传到`master`分支

开始部署：

```shell
hexo clean # 清理缓存
hexo g # 生成静态文件
hexo s # 本地预览
hexo d # 部署（跟 _config.yml 文件中的 deploy 选项相关）

```

本地预览：

![image-20210506120027729](/images/github-pages-flow/08.png)

部署完成：

![image-20210506120131026](/images/github-pages-flow/09.png)

打开master分支确保最新的文件已更新

![image-20210506120254668](/images/github-pages-flow/10.png)

在Github Page 查看下效果：

![image-20210506120535125](/images/github-pages-flow/11.png)

大功告成！

以上就是发表Github Page 的常用操作，做个备忘。

参考文章：

> https://www.sulinehk.com/post/hexo-backup-reset/
>
> https://zhuanlan.zhihu.com/p/127027266
>
> https://www.cnblogs.com/ljy2013/p/5547993.html
>
> https://lvraikkonen.github.io/2016/05/31/%E5%88%A9%E7%94%A8Github%E5%88%86%E6%94%AF%E5%A4%87%E4%BB%BDHexo%E6%BA%90%E6%96%87%E4%BB%B6/