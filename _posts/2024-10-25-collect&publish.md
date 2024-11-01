---
title: 从网站收藏到自动发布
layout: post

---
在网络冲浪的过程中，每当发现一个出色的网站，我们通常会将其添加到书签中以备日后访问。然而，随着时间的推移，这些书签可能会变得难以管理，以至于我们既难以再次访问它们，也难以回忆起它们各自的内容。

近日遇到了一个很有启发性的项目，该项目利用 Notion 作为信息存储的源头，并通过 GitHub Action 的自动化流程，将这些信息转换成 Markdown 文件。最终，这些 Markdown 文件被用来生成一个网站。简而言之，就是将 Notion 中的内容自动化地转换成了一个可浏览的网站。

其运作机制如下：
1. 用户通过安装并使用[ save-to-notion](https://chromewebstore.google.com/detail/save-to-notion/ldmmifpegigmeammaeckplhnjbbpccmm)浏览器插件，可以方便地将心仪的网站快速保存到Notion平台上。
2. 这些保存在Notion数据库中的网站信息，随后会被GitHub Action这一自动化工具捕获并处理。GitHub Action会将这些信息转换成Markdown格式的文件，这些文件是构建网站所需的基础素材。
3. 最后，借助Vercel这一强大的部署平台，这些Markdown文件被进一步转化为一个完整的、可访问的网站，并且能够实现自动化的更新与发布。每当Notion中的数据发生变动时，网站的内容也会相应地进行更新。

Refer：
https://github.com/thinkerchan/notion2md
https://github.com/thinkerchan/weekly/

Demo：
[https://wk.hijoe.net/](https://wk.hijoe.net/)

![2024-10-05-15518.png](http://hijoe.net/assets/2024-10-05-15518.png)
