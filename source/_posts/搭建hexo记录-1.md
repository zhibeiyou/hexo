---
title: 使用hexo+GitHub搭建博客记录
date: 2018-04-25 18:50:37
tags: [hexo,github,npm,基础]
categories: 搭建博客
keywords: [hexo,github,npm,基础]
---
一步一步搭建自己的博客(基础)
 <!--more-->
 

 ### 搭建博客记录(1)文章转载于：
 [http://www.cnblogs.com/fengxiongZz/p/7707219.html](http://www.cnblogs.com/fengxiongZz/p/7707219.html)

 ### 搭建博客记录(2)文章转载于：
 [http://www.cnblogs.com/fengxiongZz/p/7707568.html](http://www.cnblogs.com/fengxiongZz/p/7707568.html)

 ### 搭建心得
 1. 使用leancloud云储存做文章阅读次数的存放
 2. 使用来必应做博客评论模块
 3. `hexo new page "fileName"` 在网站根目录source下创建文件，并在该文件底下创建index.md。若要将其作为什么模块用的话，需要添加`type:模块名称`。如about(关于我)的模块，需如下步骤：
 	* 在hexo控制台环境下，键入`hexo new page "about"`
 	* 在主题根目录下修改_config.yml中menu标签下的about标签，并将其设为`about:/about/ || user`。
 	* 如果你的网站根目录下的_config.yml中的language的值有设为zh-Hans的话，我们需要到主题根目录下的language文件夹中找到zh-Hans.yml文件并修改其中的menu下about的值为"关于我"
 	* 最后一步，修改网站根目录下的about文件夹中的index文件，在其开头中写入`type:about`。到此我们的博客上就可显示出“关于我”的模块。
 4. 在markdown中文章开头添加一个简短的摘要，并在摘要其下写入`<!--more-->`，这样我们的文章就不会统统显示出来，而是需要点击阅读全文才能全部显示。
 5. 为文章添加标签，在其头部中添加，例：`tags: [hexo,github,npm,基础]`，添加分类，例：`搭建博客`。

 
 
 
 

 