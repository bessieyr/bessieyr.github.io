---
title: 我的blog建立指南
date: 2020-05-04 19:14:20
tags: Hexo
mathjax: true
---

# 我的选择

该怎么说呢，最初用上hexo，只是单纯的希望能便捷的建立一个私人的资料库。但是逐步地发现，hexo就好像个深不见底的地洞，初看以为不过就这点东西，没什么稀奇的，再看就觉得要命，这根本是个通向另外个星球的隧道吧！

有很多实用的外挂工具，诸如是latex、gitalk等，都是可以跟hexo联系起来使用的，所以本篇的重心不会完全专注于hexo本身，而是从某一个需要的功能出发，进而连结到更多可延伸探讨的工具。我会罗列出我所认为非常有用的工具，至于使用的方法则更多地是放上网络链接，因为网上已有很多大神对使用做出了详尽的解释与说明，相信若是有一个更完整的数据整理库的存在便能帮助大家指引出一条清晰地道路。



# 建立部落格

## 基本搭建：Github Pages + Hexo + Next

- **Github Pages：**建立属于我们的站点 ✐ [github pages使用入门](https://docs.github.com/cn/free-pro-team@latest/github/working-with-github-pages/creating-a-github-pages-site)

- **Hexo：**作为blog的基本架构，安装hexo后输入一些简单的cmd指令就可以将blog部署到github pages
- 如果想要了解hexo的基本核心，清楚指令背后的意义请参阅 ✪ [Hexo官方API](https://hexo.io/docs/)
  - 对那些基本定义不太感兴趣，这里是直接的干货指引 ✐ [如何使用Hexo创建个人博客](https://www.jianshu.com/p/e9aa00eb24bc)
  - 如果对于如何用Github Pages + Hexo建立部落格还是晕晕乎乎弄不太清楚，没事，这里还有大神手把手包教包会，甚至还附带了建立完后的网站<font color="red">优化设定</font>! ✐ [超详细Hexo+Github Page搭建技术博客教程【持续更新】](https://segmentfault.com/a/1190000017986794) 
- **Next：**针对hexo的主题美化，一个\next\_config.yml文件，搞定blog的所有外观设定！爸爸再也不用担心我看不懂js、css、html等一系列衍生出的各种电脑语言啦~ **指路** ✪ [Next官方教程](https://theme-next.iissnan.com/getting-started.html) ✪ [Next的Github站点](https://github.com/theme-next/hexo-theme-next)
  - Hexo的衍生出的主题是用很多的，甚至你也可以自己写一个Hexo出来。但个人还是推荐Next，毕竟维护人员多使用人员多各种东西使用起来都比较有保障。
  - 比较霸气粗犷的个性化教程：[hexo的next主题个性化教程:打造炫酷网站](https://upload.jianshu.io/users/upload_avatars/5308475/e6473249-62eb-4752-91b4-5fc9f2da8cf9.jpg?imageMogr2/auto-orient/strip|imageView2/1/w/80/h/80/format/webp)
  - 比较温柔秀气的个性化教程：[HEXO搭配主題next基礎配置教學](https://blog.typeart.cc/HEXO%E6%90%AD%E9%85%8D%E4%B8%BB%E9%A1%8Cnext%E5%9F%BA%E7%A4%8E%E9%85%8D%E7%BD%AE%E6%95%99%E5%AD%B8/)



## 一些我所遇到的坑与建议(Next：v8.0.2)

- Next主题顶部黑边问题
- git deployer not found
- 可能有些啰嗦的建议



**Next主题顶部黑边问题**

查看\next\_config.yml文件，取消注释：

```yml
# Define custom file paths.
# Create your custom files in site directory `source/_data` and uncomment needed files below.
custom_file_path:
  #head: source/_data/head.swig
  #header: source/_data/header.swig
  #sidebar: source/_data/sidebar.swig
  #postMeta: source/_data/post-meta.swig
  #postBodyEnd: source/_data/post-body-end.swig
  #footer: source/_data/footer.swig
  #bodyEnd: source/_data/body-end.swig
  #variable: source/_data/variables.styl
  #mixin: source/_data/mixins.styl
  style: source/_data/styles.styl #这是我们在这里需要用的文件，取消它的注释
```

在新版的Next中，支持推荐将个人的custom files与next的文件分开，custom file存储位置：根目录/source

在该位置下新建_data文件夹，进入文件夹，再新建styles.styl

修改styles.styl文件，添加代码：

```css
.headband {
    display: none
}
```

如果有发现类似于这种的黑方框问题，都可以用这种方法解决。从测试网页的源代码找出它的class name之后取消显示就行。



**git deployer not found**

这个问题一般在新手第一次按教程大礼包建立网站时是不会发生的，而是发生在自己摸摸索索地hexo新建了个资料夹后发现，诶介个资料夹怎么跟上个不一样？傻乎乎的，其实不过就是环境还没安装好，没下载hexo-deployer而已。

issue指路 ✄ https://github.com/hexojs/hexo/issues/1040



**可能有些啰嗦的建议**

这里不建议<font color="red">直接</font>对原本的next主题文件进行大规模修改，毕竟使用next的优势就是它会不断更新完善，如果对内部进行修改，就会不易于去更新next，反而丢失了它的这项优势。另外，如果是对代码和主题文件并不太了解的孩子们，next的代码结构我认为是比hexo自带主题要繁琐的，因此更建议先从hexo原生的自带主题landscape了解起会更好，虽然了解清楚这些架构在我看来其实都并没有什么多大卵用，这很可能是道花时间而不讨好的工序。

以下放上一些过去在**使用hexo原生主题landscape**的各种心路历程，存在资料已经过时的可能：

- 使用[toc功能](https://hexo.io/docs/helpers#toc)，将sidebar做成书页目录。<br>值得一提的是，`<%#- partial('_partial/sidebar', null, {cache: !config.relative_link}) %>`中的`null`要去掉，否则sidebar会是在原有的内容上添加文字

- 添加latex: [参考资料](https://cps.ninja/2019/03/16/hexo-with-latex/)

- 添加[gitalk评论](https://gitalk.github.io/)，可以懒人模式地使用latest来得到最新版本`<script src="https://unpkg.com/gitalk@latest/dist/gitalk.min.js"></script>`

- 添加[mermaid]( https://mermaid-js.github.io/mermaid/#/)，

- ~~试图在visual studio使用latex，但是由于latex发行版文件过大而暂时停滞~~

- 为blog文章添加更新时间：[参考资料](https://github.com/hexojs/hexo/issues/3094)

- 添加local-search功能<br>如果只是想简单套用一个搜索插件代码的话可以参考Liam大神发布的资料，使用的帮助插件是[hexo-generator-search](https://github.com/wzpan/hexo-generator-search)

  如果和我一样有强迫症偏好使用更新颖完善的插件[hexo-generator-searchdb](https://github.com/theme-next/hexo-generator-searchdb)的话，提前了解[配置信息如何交互](https://liuyib.github.io/2019/08/20/develop-hexo-theme-from-0-to-1/)是非常重要的，这可以处理`global CONFIG`的需求。~~未来也许可能觉得必要的话会整理出我的编写档案

- [想给你的网页加上酷炫动效？这有 20 个神器帮你！](https://www.uisdc.com/dynamic-animations-ui)



# 编辑部落格

## 私心推荐的工具搭配：Typro+PicGo+cdn

要编辑blog通常听起来不是什么麻烦事，不就是写文嘛？有什么难的！

这就要说到github支持的语法规范是markdown，一种使用惯了后就再也看不上其他写作方式的语法（捂脸）

markdown的特点就是直接用符号的输入来表示我们在日常对字体格式的输入，更加地直接暴力简洁！

但是这种简洁快速也是需要搭配好的软件来支持，以下是我日常使用的组合：**Typro+PicGo+cdn**

- **[Typro](https://typora.io/)：**markdown即时渲染编辑器。真的炒鸡好用！界面干净，输入起来比word还要快速流畅，达到我写即我思的效果。
- **[PicGo](https://molunerfinn.com/PicGo/)：**用于将typro上的图片快速上传至云端并取得url连接使用于部落格中
- **cdn：**用于浏览页面时图片的加速，主要针对于图片上传至海外图床，由于一些不可告人秘密，导致国内使用时会很卡的情形
- 保姆级教程 ✐ [使用Picgo+GitHub+ jsDelivr搭建CDN加速免费图床](https://my.oschina.net/u/4131402/blog/4373012)
- Typro的偏好设定大致上如下图就行

![image-20201114171836942](https://cdn.jsdelivr.net/gh/ronyeaf/asset/img/20201114182946.png)



## PicGo排坑

我开始使用picgo的时候，picgo开发可能还不算稳定吧，所以运行时会有不少的问题。

不确定现在的picgo是否有将这些问题解决完善，但是这边提供一个可能的解决思路。

1. 检查picgo设置中的设置服务，地址与端口是否与下图一至。

![image-20201114170748856](https://cdn.jsdelivr.net/gh/ronyeaf/asset/img/20201114183016.png)

2. 检查是否有开启时间戳重命名，没开启的话可能会发生图片修改后再上传但却因重名而产生有图片被遗漏的bug。

![image-20201114171028768](https://cdn.jsdelivr.net/gh/ronyeaf/asset/img/20201114183017.png)

3. 直接查看它的日志去了解是哪里运行时出了问题。



# 云端部落格与本地资料同步

这一部分存在的意义，对其他人来说可能是为了方便多云端同步或者想要个云端存储库之类的，但对我来说只是纯粹强迫症与龟毛主义。

不知道有没有小伙伴和我一样，真的很嫌弃cmd的小黑框界面，很讨厌hexo s+hexo deploy+hexo g的部署上传模式。真的，宁愿上网站去干净的界面点击图标上传，而不愿意碰触这些由英文字母组成的指令。很奇怪吧，虽然说耗费时间上算起来可能差不多，但就是被新时代的漂亮UI设计养成了这些坏毛病。

实现云端部落格与本地资料同步后，就可以直接使用github桌面软件，将更新的档案按按钮push一下就行，更符合现下的操作美学。

方法主要是：**Clone + GitHub Actions** 

- **Clone：**在github仓库中新建一个hexo分支，通过克隆的方式，让这个分支能和本地的hexo站点资料库同步。难度不大，主要是需要熟悉github的仓库操作管理，实现思路可参考 ✐ [Hexo博客在多台终端同步管理](https://www.jianshu.com/p/937bda9123da)
- **GitHub Actions：**使用actions让同步后的hexo分支自动向master部署网站。知乎的这位大神写得真的很好，步骤清清楚楚，照着做下来没什么问题 ✐ [GitHub Actions 自动部署 Hexo](https://zhuanlan.zhihu.com/p/133764310) ✪ [官方指南](https://github.com/marketplace/actions/hexo-action)
- 排坑：这是在最终push时可能会发生Next主题文件无法上传的问题，请参考issue ✄ [主题文件无法同步的问题 #734](https://github.com/litten/hexo-theme-yilia/issues/734)，如果其中有什么问题可使用`git status`先查看文件状态，确认是否有文件误被ignore



