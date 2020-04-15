---
title: Valine Admin 发送的邮件中的链接无法打开
date: 2020-04-08 12:13:57
tags: [blog,踩坑]
category: 
- [Tech,Blog]
---

Valine Admin 是 Valine 的修改版，相比原生 Valine 邮件通知功能更完善。原 Valine 发送的通知邮件里的按钮只能到达博客首页，无法到达相关文章页面；Valine Admin 还加入了垃圾评论过滤功能。

在部署 Valine Admin 后，测试评论系统时，发现收到的通知邮件里的链接点击无效，无论是「查看回复的完整内容」还是开头的 blog 名。

换邮箱、换 SMTP 服务器都无果，**最后发现在云引擎的自定义环境变量中，「SITE_URL」值里的域名应该加上 https:// ，之前填写的是「yobome.top」，在换成「https://yobome.top」之后，重启实例**，成功。