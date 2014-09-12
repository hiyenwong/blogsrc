---
layout: post
title: "制作octopress"
date: 2014-08-30 11:37
comments: true
categories: [octopress,github.com]
---

#octopress的部署

##关于octopress的安装

git octopress

```
git clone git://github.com/imathis/octopress.git  YOUR_DIR

```

你需要在github页面上的account设置SSH的public key, 所以你这必须是使用`ssh-keygen`生成public key

并且为了保留原先的markdown文件,所以可以另外设置一个repository,然后设置以下remote,这样可以保留原先的原始文件和修改内容.

另外我们需要安装所需的gem,运行命令`bundle install`,就可以将Gemfile里的列表安装到电脑里.

##设置基本的octopress

设置octopress很简单,只要使用两步.

设置你的repository,打命令 `rake setup_github_page`

然后我们只要设置一下配置文件_config.yml就完美了.

##发布你的博客

###新建博客: 
`rake new_post[post_name]`

###生成静态文件
`rake generate`

###发布博客
`rake deploy`

当然有时,rake的版本不对,没关系,你可以使用`bundle exec`来避免这样的问题.


