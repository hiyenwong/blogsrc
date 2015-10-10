---
layout: post
title: "GOLANG在Fedora21上的部署"
date: 2015-02-19 20:34
comments: true
categories: [fedora,golang]
---
#Golang 在Fedora21上安装
Fedora21本身就提供了Go的1.3.3版本，虽然没有最新的1.4，但对于开发学习绰绰有余。由于Golang.org等一系列Google服务器被墙，所以`go get`获取golang.org 资源比较吃力。好在Fedora21镜像自身提供了一些Googlecode上的安装包，因此你只要yum 搜索一下就知道了。

##关于Go的环境变量
通过yum安装之后，有几个环境变量是没有设置，比如最重要的$GOPATH,还有$GOROOT和$GOBIN.这些之所以要设置这几个环境变量，是因为在开发中我们会经常用到。

###$GOROOT
`GOROOT`主要是设置为go的安装源代码路径，Fedora21的默认安装路径在`/usr/lib/golang`

###$GOPATH
`GOPATH`主要是设置Go的开发路径，通常你将在这个路径下进行开发，开发的目录结构则必须包括`pkg`,`src`,`bin`。通常bin则是存放程序编译之后的执行文件。

###$GOBIN
`GOBIN`为执行文件路径，如果你是管理员权限，可以将路径设置为`/bin/`或是`/usr/bin`，当然你如果不是管理员权限，完全可以设置为`$GOPATH/bin`,最重要的是这样设置之后，必须你将它加入到`$PATH`里去。

#关于Go的包安装
一直都不太喜欢go的包管理，主要因为是它没有像ruby那样的方便搜索和版本管理，而且go的包一部分存放在google的服务器上，给下载造成一定困难。特别在包依赖的情况下，你必须另找途径一个个安装。目前除了自己翻墙的解决方法以外，你可以搜索github上的资源单独下载。

##关于Go的IDE
Go的IDE还是比较多的，最常用的可能是sublime text和vim。 sublime text并没有open source,因此我选择了github的atom和vim。

###vim
vim的基本插件，yum里有，所以很容易安装，当然懒人总有很多懒人办法，我这里使用的是janus的管理，这使得管理插件更方便，直接clone到.janus目录就可以。
###atom
atom上的有一个golang-plus的插件用于go的开发，但其中需要安装一些go的扩展，主要有如下几个
- gocode 用于自动补全，这个github上有
- goimports 这个在github上也有
- lint tools 这个需要翻墙安装，否则依赖你要自己找第三方下
- goimports 这个包在Fedora21里有，可以直接下载。

基本Golang的开发环境就这些，接下来就是学习的过程。
