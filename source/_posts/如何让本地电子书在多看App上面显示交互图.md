---

title: 如何让本地电子书在多看App上面显示交互图
date: 2020-12-07
---

我常年使用**多看App**看书，付费买过很多的书。

这几年，**多看书城**不是很争气，**新书**越来越少。

但是，即便如此，作为一个喜欢折腾电子书的人，各种App我都使用过。最后还是认为多看书城的书排版是最好的。图文并茂，而且图片可以用两指缩小放大，可以看清楚很多图片的细节。文字间距的调整也很舒适。总之，用久了，已经习惯了，已经离不开了。

有时候，想要看的图书资源书库里面没有，我也就在其他书城里面看下。

如果连其他书城也没有，那我只能自己去查找，然后导入多看App，最终还是在多看里面阅读。

在我看来，即使只把多看App 当做一个**离线阅读器**，只阅读**本地书**，它的体验也是很优秀的。



不过多看有一个缺点，很多通用格式的epub电子书，里面的图片在多看App里面是不能放大的。

我最近在学习Python，很多教程的图片，如果不放大，那么是看不清代码的细节的。

于是，只能去查找教程，修改一下epub文件的图片排版。



下面我把我的折腾过程，写一下：



这是我下载的一本电子书，图片不能直接点击放大，在需要看清细节的时候很不方便。

所以，只能自己用Sigil修改下。



![](/images/2020-12-07/01-epub-no-zoom.jpg)
关于**Sigil:**

> **Sigil**是一款[EPUB](https://zh.wikipedia.org/wiki/EPUB)[电子书](https://zh.wikipedia.org/wiki/電子書)制作软件及[开源](https://zh.wikipedia.org/wiki/开源软件)EPUB电子书编辑器，支援[Windows](https://zh.wikipedia.org/wiki/Windows)、[Linux](https://zh.wikipedia.org/wiki/Linux)和[Mac](https://zh.wikipedia.org/wiki/Mac)系统。Sigil使用[CSS](https://zh.wikipedia.org/wiki/CSS)和[HTML](https://zh.wikipedia.org/wiki/HTML)格式，拥有[所见即所得](https://zh.wikipedia.org/wiki/所見即所得)界面，并有自动生成目录、自动修正等功能。

如果你对本地的电子书有排版上面的不满，Sigil绝对可以帮上你的忙。排版神器。

但是刚开始可能要找个教程了解一下。

网友Zecy有不错的教程：（Zecy分享的链接找不到了，这是B站上面的一个），入门Sigil很合适。

https://www.bilibili.com/video/av32221153/



打开图书后，在**Sigil**里面显示是这样的：

![Snipaste_2020-12-06_18-16-54](/images/2020-12-07/02-sigil-open.jpg)



我们要把图片修改成多看自带的**交互图**方式。

交互图的介绍：



> 交互图主要实现用户点击图像后，图像自动全屏显示，在全屏显示时图像可以两指放大和旋转。
>  实现方法只需要加上duokan-image-single这个类即可。当然在CSS里也可以针对此类自定义样式。

主要的代码：

```css
<div class="duokan-image-single">
    <img src="../Images/pic.png" alt="" />
    <p class="duokan-image-maintitle">主标题</p>
    <p class="duokan-image-subtitle">副标题</p>
</div>

```

既然要修改的是图片，就要找出电子书中图片出现的规律

本书图片在Sigil里面显示是这样的：



![](/images/2020-12-07/03-sigil-images.jpg)

我们只需要保留最重要的**图片路径**以及**图片描述**就够了：

`<img src="../Images/00003.jpeg" `是图片路径

`<h6 class="calibre26"><span class="keep-together">Figure 2-3. </span>Jupyter example view for an existing notebook</h6>`是图片的描述，最重要的是其内容：`Figure 2-3. Jupyter example view for an existing notebook`，其他有关样式的东西其实可以舍弃。



由于一个一个修改这种文本太过麻烦，我们使用**正则表达式**直接批量修改。

**正则表达式**绝对是你短时间内能学会然后就可以受用无穷的东西，关于**查找**、**替换**，很多复杂的需求都可以用简单的语句来表达。绝大多数常用的文本编辑器和IDE在搜索框里面都会提供**正则**搜索选项的。你学会之后，就可以一直与它为伴了。

送你一个**Sigil**正则表达式入门教程：

https://web.archive.org/web/20150906124319/http://anipv.info/blog/sigil-regexp-intro

这个也很不错：

https://tieba.baidu.com/p/3493107610?fr=good

这里不细讲。文章写的很具体，绝大多数常用电子书排版技巧都有涉及。有兴趣可以自行阅读。

我们只讲我遇到的添加交互图代码的修改过程。

由于涉及多行替换，我们得使用`(?s)`

> (?s)放在表达式的最前端，使得“.”可以匹配到“\n”，从而实现跨行匹配。
>
> 比如以下例子：
>
> `<div></div>`
>
> `<h1></h1>`
>
> `<div></div>`
>
> 使用正则表达式`“<div>.*</div>”`一次只能匹配到第一行或者第三行。
>
> 而使用`“(?s)<div>.*</div>”`则能一次性匹配到第一行到第三行所有内容。

**查找语句**：

`(?s)<figure.*?<img src="(.*?)".*?(Figure.*?)</span>(.*?)</h6.*?</figure>`

**替换语句：**

`<div class="duokan-image-single">\n<img src="\1" alt="" />\n<p class="duokan-image-subtitle">\2\3</p>\n</div>`

查找语句中除了`(?s)`以外，3个`()`里面的内容是我们要保留的内容，其他的舍弃。

替换语句中`\1\2\3`对应着上面3个`()`，把内容填入新的语句。

这个时候**Sigil**搜索框显示是下面这样的，文字变蓝说明正则语句查找到了我们想要替换的语句。

![image-20201206201013373](/images/2020-12-07/04-sigil-find.jpg)



如果选中所有HTML文件，然后选中**计数所有**，显示有70个匹配，与电子书中的图片数量匹配，说明这个查找语句可以适合本书所有图片。

 ![image-20201206202013465](/images/2020-12-07/05-sigil-count.jpg)



但是，我们还是只先替换一张图片，点击**替换**

替换之后是这样的：

![image-20201206202257043](/images/2020-12-07/06-sigil-replace.jpg)

没问题，那就把其他的图片也替换了。

导出电子书，在多看上面打开看看。



![](/images/2020-12-07/07-duokan-1.jpg)

![](/images/2020-12-07/08-duokan-2.jpg)

![](/images/2020-12-07/09-duokan-3.jpg)
图片可以放大了。完成。



这个修改图片的方法我经常使用，但是过段时间不用又得找教程折腾一下，今天又用了一次，就把过程记录下来了。当作备忘吧.



当然，得注意，这本书的格式肯定与其他书有很多不同，所以查找替换图片的语句不用直接拿去用，但是原理是类似的，只要弄懂了查找替换正则表达式的意义，稍微修改下，就能用了。



有什么错误或者更好的方法，欢迎交流，谢谢！





