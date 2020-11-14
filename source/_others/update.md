---
title: 更新日志
date: 2020-05-03 20:18:13
categories: Others
---

# 2020

- 建立初始网站页面<br>排坑：[git deployer not found](https://github.com/hexojs/hexo/issues/1040)
- 使用[toc功能](https://hexo.io/docs/helpers#toc)，将sidebar做成书页目录。<br>值得一提的是，`<%#- partial('_partial/sidebar', null, {cache: !config.relative_link}) %>`中的`null`要去掉，否则sidebar会是在原有的内容上添加文字
- 使用typro：markdown编辑器 + picgo：图片上传 + cdn：加速，进行blog的书写<br>其中建议阅览[picgo的教学](https://zhuanlan.zhihu.com/p/114175770)，这相当有助于排坑
- 添加latex: [参考资料](https://cps.ninja/2019/03/16/hexo-with-latex/)
- 添加[gitalk评论](https://gitalk.github.io/)，可以懒人模式地使用latest来得到最新版本`<script src="https://unpkg.com/gitalk@latest/dist/gitalk.min.js"></script>`
- ~~添加[mermaid]( https://mermaid-js.github.io/mermaid/#/)，但由于书写上不够便利，功能上又尚在更新，导致新功能无法在typro编辑器上照常显示等原因而又删除~~
- ~~试图在visual studio使用latex，但是由于latex发行版文件过大而暂时停滞~~
- 为blog文章添加更新时间：[参考资料](https://github.com/hexojs/hexo/issues/3094)
- 添加local-search功能<br>如果只是想简单套用一个搜索插件代码的话可以参考Liam大神发布的资料https://github.com/Liam0205/hexo-search-plugin-snippets，使用的帮助插件是[hexo-generator-search](https://github.com/wzpan/hexo-generator-search)<br>如果和我一样有强迫症偏好使用更新颖完善的插件[hexo-generator-searchdb](https://github.com/theme-next/hexo-generator-searchdb)的话，提前了解[配置信息如何交互](https://liuyib.github.io/2019/08/20/develop-hexo-theme-from-0-to-1/)是非常重要的，这可以处理`global CONFIG`的需求。~~未来也许可能觉得必要的话会整理出我的编写档案

https://pixabay.com/photos/jellyfish-aquatic-animal-ocean-2566795/

[想给你的网页加上酷炫动效？这有 20 个神器帮你！](https://www.uisdc.com/dynamic-animations-ui)

[哪些图片网站可以免费使用图片，不用担心版权问题？](https://www.zhihu.com/question/51972115)

[2020年第一波实用设计工具合集](https://www.uisdc.com/26-tools-to-start-off-2020)



