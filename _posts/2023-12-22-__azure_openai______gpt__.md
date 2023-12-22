---
layout: post
title: 使用Azure OpenAI构建私人聊天GPT界面

---
网上有不少利用OpenAI构建私人聊天GPT界面的文章，不过鉴于OpenAI账号申请和访问难度，利用Azure OpenAI来构建私人GPT有一定优势。<br>
如何申请Azure OpenAI可以自行百度，下面介绍一下如何利用Vercel免费搭建私人GPT界面。<br>

源码参考：https://github.com/mckaywrigley/chatbot-ui <br>
Deploy by Vercel：
[![2023-12-05-774375.svg](http://hijoe.net/assets/2023-12-05-774375.svg)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2Fmckaywrigley%2Fchatbot-ui)<br>
重点：部署成功后须在项目的Settings-->Environment Variables下添加相关变量。<br>

![2023-12-05-952488.png](http://hijoe.net/assets/2023-12-05-952488.png)<br>
其中OPENAI_API_KEY，AZURE_DEPLOYMENT_ID和OPENAI_API_HOST需从Azure OpenAI Playground平台内获取。<br>

![2023-12-05-809711.png](http://hijoe.net/assets/2023-12-05-809711.png)<br>
最后，记得在Vercel的Settings-->domains绑定域名，这样你就能愉快的使用您的私人GPT了。<br>

![2023-12-05-147628.png](http://hijoe.net/assets/2023-12-05-147628.png)


