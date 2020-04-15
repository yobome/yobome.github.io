---
title: Next 升级小记
date: 2020-04-08 01:12:43
tags: [blog,踩坑]
category:
- [Tech,Blog]
---

由于一开始搭建的博客 Next 主题版本较老（5.1.4），会与一些插件的新版本出现兼容性问题，如 Valine 的 Visitor 无法显示。于是打算将 Next 升级到最新的 7.8.0 版本（较新的 Next 版本号已经无法在主题配置文件下查看，这里可以查看主题文件夹下的 package.json 文件）

## 步骤

### 克隆新版 Next 库

在博客根目录下运行如下指令，其中后面的 "themes/next-reloaded" 为目标文件夹，可以自主命名，但必须在 themes 文件夹下

    git clone https://github.com/theme-next/hexo-theme-next themes/next-reloaded

### 修改配置文件

#### 修改博客配置文件 (your_blog_path/_config.yml)

    theme: next-reloaded

#### 修改主题配置文件 (.../themes/next-reloaded/_config.yml)

这里按照个人的插件配置、喜好来修改，附上我的修改：

    #关闭页面下方的「由 Hexo 驱动」等信息
    powered: false

    #选择主题
    scheme: Gemini

    #导航菜单设置
    menu:
      home: / || fa fa-home
      categories: /categories/ || fa fa-th
      tags: /tags/ || fa fa-tags
      archives: /archives/ || fa fa-archive
      about: /about/ || fa fa-user

    #页面宽度，Gemini 的默认宽度为 240
    width: 300

    #开启 fancybox
    fancybox: true

    #开启评论系统与阅读量统计
    valine:
      enable: true
      appid: your_app_id
      appkey: your_app_key
      notify: true 
      verify: false 
      placeholder: Comment Here~ 
      avatar: retro 
      guest_info: nick,mail,link 
      pageSize: 10 
      language: 
      visitor: true 
      comment_count: true 
      recordIP: false 
      serverURLs: 
      #post_meta_order: 0

    #开启访客统计
    busuanzi_count:
      enable: true
      total_visitors: true
      total_visitors_icon: fa fa-user
      total_views: true
      total_views_icon: fa fa-eye
      post_views: false
      post_views_icon: fa fa-eye

    #开启搜索插件
    algolia_search:
      enable: true

    #更换 js 的 cdn
    fontawesome: //cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@5/css/all.min.css

    jquery: //cdn.jsdelivr.net/npm/jquery@3/dist/jquery.min.js
    fancybox: //cdn.jsdelivr.net/gh/fancyapps/fancybox@3/dist/jquery.fancybox.min.js
    fancybox_css: //cdn.jsdelivr.net/gh/fancyapps/fancybox@3/dist/jquery.fancybox.min.css

    lazyload: //cdn.jsdelivr.net/npm/lozad@1/dist/lozad.min.js

    valine: //cdn.jsdelivr.net/npm/valine@1/dist/Valine.min.js

    algolia_search: //cdn.jsdelivr.net/npm/algoliasearch@4/dist/algoliasearch-lite.umd.js
    instant_search: //cdn.jsdelivr.net/npm/instantsearch.js@4/dist/instantsearch.production.min.js

    velocity: //cdn.jsdelivr.net/npm/velocity-animate@1/velocity.min.js

    velocity_ui: //cdn.jsdelivr.net/npm/velocity-animate@1/velocity.ui.min.js


## 踩坑

1. Valine 评论开启后，标题下方显示的是「Valine: 0」而不是「评论数：0」
   - 在主题文件夹下的 languages 文件夹中，修改 zh-CN.yml，在 "post:" 下添加子字段 "comments.valine: 评论数"

2. symbols_count_time 在开启后显示「阅读时长 ≈ NaN:aN」
   - 在博客配置文件下添加如下字段：
    ```yaml
    symbols_count_time:
    symbols: true    #显示文章字数
    time: true    #显示文章所需阅读时间
    total_symbols: true    #在页面底部显示网站文章总字数
    total_time: true    #在页面底部显示网站总阅读时间
    ```
   - 在主题配置文件下添加如下字段：
    ```yaml
    symbols_count_time:
    separated_meta: true
    item_text_post: true    #标题下方显示文章字数
    item_text_total: false    #标题下方显示网站总字数
    #如果是中文博客，官方建议以下数值分别设置为 2、300
    awl: 4    #默认字符长度 Average Word Length，中文为2。
    wpm: 275    #默认阅读速度 Words Per Minute
    ```

大功告成！如果还有什么遗漏的地方想到了再补充，有问题欢迎留言或者邮箱联系我。