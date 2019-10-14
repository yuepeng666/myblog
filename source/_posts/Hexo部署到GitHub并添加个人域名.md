---
title: Hexo部署到GitHub并添加个人域名
date: 2019-06-14 11:11:58
categories: hexo 随笔
tags: hexo
---

<meta name="referrer" content="never">

### 域名

1. 从[freenom](https://www.freenom.com/zh/index.html?lang=zh)获取免费域名

2. 添加域名解析:

![](https://ws1.sinaimg.cn/large/005R0tlAly1g40iod34m2j30v40cmnka.jpg)

 <!-- more -->

点击 ManageDomain>> ManageTools >> Nameservers

![](https://ws1.sinaimg.cn/large/005R0tlAly1g40ir182m7j30nr0htglu.jpg)

在图示位置添加域名解析服务（本文使用 DnsPod 做域名解析）

```
f1g1ns1.dnspod.net

f1g1ns2.dnspod.net
```

3. 注册并登陆 DnsPod, 点击添加域名添加你申请的域名，点击已域名，随后点击添加记录

![](https://ws1.sinaimg.cn/large/005R0tlAly1g40iy6dov1j30rb090gly.jpg)

4. 主机记录：@， 记录类型： A，记录值： （ping 你的 github 账号获到取的 ip）

   `ping githubname.github.io`

5. 主机记录：www， 记录类型：CNAME，记录值：
   `yourgithubname.github.io`

6. 其他操作如图

   ![](https://ws1.sinaimg.cn/large/005R0tlAly1g4d76ixx4tj30s00n5aat.jpg)

### 绑定域名

1. 在 hexo/source/目录下新建 CNAME 文件(必须大写)
   ![](https://ws1.sinaimg.cn/large/005R0tlAly1g4d790t28lj308o0aggln.jpg)

1. 打开 CNAME 文件在里面填入你获取到的域名

1. 打开编辑\_config.yml 在图示位置添加你的 github 项目地址

![](https://ws1.sinaimg.cn/large/005R0tlAly1g4d7quhnayj30jb0e1t96.jpg)

1. 运行如下命令部署 blog 到 github

   `hexo clean`

   `hexo d`

1. 打开 github 项目进行如下操作

![](https://ws1.sinaimg.cn/large/005R0tlAly1g4d7df01oxj30ti0mdmy9.jpg)

![](https://ws1.sinaimg.cn/large/005R0tlAly1g4d7e33ydcj30rl0kgq40.jpg)

1. 完成
