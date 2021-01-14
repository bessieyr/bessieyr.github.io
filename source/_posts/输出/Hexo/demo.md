---
title: Demo 测试
date: 2020-05-01 17:59:42
tags: Hexo
---

# 前言
This is a demo.
这是测试文。

# Title
# H1 标题
## H2 标题
### H3 标题
#### H4 标题
##### H5 标题
###### H6 标题
====== 标题
------ 标题
显然 - & = 号并不适合作为hexo系统下的标题的选择

# 字效
*斜体* **加粗** ~划线~

# List
1. 序列number1
2. 序列number2
  - sublist by -
  + sublist by + 
  * sublist by *
  1. sublist

    - sub
      - sub
        - sub
          - sub
            - sub
              - sub
                - sub
                  - sub

- [ ] 选框

- [x] 复选框

# 上下标

H<sub>2</sub>

H<sup>2</sup>

# 链接

[链接]
[链接：百度一下](www.baidu.com)
[链接：google][www.google.com]
[link1][1]
可以事后再对link进行补充
[1]: www.blank.com
[链接]: www.blank.com
## 尝试
立刻带积分
# 图片Images
Inline-style: 
![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1")
Reference-style: 
![alt text][logo]
[logo]: https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 2"

# Code
`Code Heightlight`
Inline `Code`
```html html
<link rel="stylesheet" href="/path/to/styles/default.css">
<script src="/path/to/highlight.pack.js"></script>
<script>hljs.initHighlightingOnLoad();</script>
```
```
No language indicated, so no syntax highlighting. 
But let's throw in a <b>tag</b>.
```
```js js
var a = b
var c = d
class SomeClass:
  pass
$(document).ready(function(){
  $('.main-nav-link').click(function(){
      var scrollID = $(this).attr("id").substring(1)+"-page";
      var scrollPosition = $(scrollID).offset().top;
      $('html, body, .content').animate({scrollTop: scrollPosition}, 300);
  });
}); 
```
```python python
@requires_authorization
def somefunc(param1='', param2=0):
    r'''A docstring'''
    if param1 > param2: # interesting
        print 'Gre\'ater'
    return (param2 - param1 + 1 + 0b10l) or None

class SomeClass:
    pass
```
```css css
  code
    font-size: font-size * 1.1
    line-height: text-size * line-height
    background: highlight-background
    //text-shadow: 0 1px #fff
    color: highlight-foreground
    padding: 0 0.3em
  pre
```
```css css
.article-entry
  code
    font-size: font-size * 1.1
    line-height: text-size * line-height
    background: highlight-background
    //text-shadow: 0 1px #fff
    color: highlight-foreground
    padding: 0 0.3em
  pre
```
# Table
|Table|名称|name
|---|---|---
|1|一|one
|2|二|two
|3|三|three

引用Blackquotes
> So Looooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooong
看看引用是什么样的效果

# HTML
<p>html标签是可以随便内置使用的</p>

# 水平线
---
***
水平线的使用
___

# Toggle
<details>
<summary>Click Here</summary>
  这是个可拨动的板块
  <code style="white-space:nowrap;">Toggle code</code>
</details>

```html
  <ol class="toc">
    <li class="toc-item toc-level-1"><a class="toc-link" href="#前言"><span class="toc-text">前言</span></a></li>
    <li class="toc-item toc-level-1"><a class="toc-link" href="#Title"><span class="toc-text">Title</span></a></li>
    <li class="toc-item toc-level-1">
      <a class="toc-link" href="#H1-标题"><span class="toc-text">H1 标题</span></a>
      <ol class="toc-child">
        <li class="toc-item toc-level-2"><a class="toc-link" href="#H2-标题"><span class="toc-text">H2 标题</span></a></li>
      </ol>
    </li>
    <li class="toc-item toc-level-1"><a class="toc-link" href="#字效"><span class="toc-text">字效</span></a></li><li class="toc-item toc-level-1"><a class="toc-link" href="#List"><span class="toc-text">List</span></a></li><li class="toc-item toc-level-1"><a class="toc-link" href="#链接"><span class="toc-text">链接</span></a></li><li class="toc-item toc-level-1"><a class="toc-link" href="#图片Images"><span class="toc-text">图片Images</span></a></li><li class="toc-item toc-level-1"><a class="toc-link" href="#Code"><span class="toc-text">Code</span></a></li><li class="toc-item toc-level-1"><a class="toc-link" href="#Table"><span class="toc-text">Table</span></a></li><li class="toc-item toc-level-1"><a class="toc-link" href="#HTML"><span class="toc-text">HTML</span></a></li><li class="toc-item toc-level-1"><a class="toc-link" href="#水平线"><span class="toc-text">水平线</span></a></li><li class="toc-item toc-level-1"><a class="toc-link" href="#Toggle"><span class="toc-text">Toggle</span></a></li></ol>

```
