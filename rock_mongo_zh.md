

# [我们搬家了！点这里访问新的文档！](http://rockmongo.com/wiki/introduction?lang=zh_cn) #

# 安装 #

## 需求 ##
  * 一个能运行PHP的Web服务器，比如Apache Httpd, Nginx ...
  * PHP - 需要PHP v5.1.6或更高版本，需要支持SESSION
    * 为了能连接MongoDB，你需要安装[php\_mongo](http://www.php.net/manual/en/mongo.installation.php)扩展

## 快速安装 ##

  1. [下载安装包](http://rockmongo.com/downloads)
  1. 解压到你的网站目录下
  1. 用编辑器打开config.php (v1.0.5版本以前是index.php)，修改host, port, admins等参数
  1. 在浏览器中访问index.php，比如说：http://localhost/rockmongo/index.php
  1. 使用用户名和密码登录，默认为"admin"和"admin"
  1. 开始玩转MongoDB!

## 集成环境 ##

如果没有PHP运行环境，可以在 http://rockmongo.com/downloads 下载在Windows上运行的集成环境，让你快速开始玩转RockMongo。

其他平台的运行环境可以在这里找到：
http://code.google.com/p/rock-php/wiki/RelatedProjects

## 相关文章 ##
  * [MongoDB+RockMongo安装](http://onlyzq.blog.51cto.com/1228/516623)
  * [NOSQL mongodb 安装及简介](http://www.superzc.com/archives/142)
  * [MONGODB1.8安装、分布式自动分片(AUTO-SHARDING)配置备忘](http://www.shubo.info/?tag=rockmongo)
  * [RockMongo查询操作用法总结](http://hi.baidu.com/woaidelphi/blog/item/19f07613152df19c6438db36.html)
  * [Ubuntu 10.04下安装MongoDB](http://www.mike.org.cn/articles/ubuntu-install-mongodb/)
  * [RockMongo安装与简单配置](http://hi.baidu.com/akoola/blog/item/8b0d2012069ee31e203f2e0a.html)

# 配置 #

[在这里查看配置文档](configuration_zh.md)

# 下载 #

请点击 [http://rockmongo.com/downloads](http://rockmongo.com/downloads) 下载最新的版本.

# Bug和建议 #

如果有任何Bug或者建议，请发送邮件给 iwind.liu@gmail.com ，非常感谢。

同时，我们也接收以下形式的捐助：
  * 支付宝帐号：iwind\_php@163.com
  * Paypal帐号：iwind.liu@gmail.com

在捐助后，您可以发送邮件到 iwind.liu@gmail.com 通知我们。

# 简介 #

**[RockMongo](rock_mongo_zh.md)** 是一个PHP5写的MongoDB管理工具。

主要特征:
  * 使用宽松的New BSD License协议
  * 速度快，安装简单
  * 支持多语言（目前提供中文、英文、日文、巴西葡萄牙语、法语、德语）
  * 系统
    * 可以配置多个主机，每个主机可以有多个管理员
    * 需要管理员密码才能登入操作，确保数据库的安全性
  * 服务器
    * 服务器信息 (WEB服务器, PHP, PHP.ini相关指令 ...)
    * 状态
    * 数据库信息
  * 数据库
    * 查询，创建和删除
    * 执行命令和Javascript代码
    * 统计信息
  * 集合（相当于表）
    * 强大的查询工具
    * 读数据，写数据，更改数据，复制数据，删除数据
    * 查询、创建和删除索引
    * 清空数据
    * 批量删除和更改数据
    * 统计信息
  * GridFS
    * 查看分块
    * 下载文件
  * 更多好用的特征开发中 ...

![http://ifphp.cn/rockmongo/screenshots/show.png](http://ifphp.cn/rockmongo/screenshots/show.png)