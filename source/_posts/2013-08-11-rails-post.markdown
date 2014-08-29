---
layout: post
title: "rails中post"
date: 2013-08-11 22:15
comments: true
categories: ['rails','ruby','post','mvc','controller']
---

#Form Helper basic#
view中设置其表单，其中`form_tag`定义提交给谁和用什么方法
``` ruby Form表单提交给helo
<%= form_tag("helo",method: 'post') do %>
<%= label_tag(:search, "search for:") %>
<%= text_field_tag(:search) %>
<%= submit_tag("Search") %>
<% end %>
```

#Controller 如何实现接受#

在接收的方法中使用`params[:search]`
``` ruby Controller中抓去post值
def helo
@helo=params[:search]
end
```


#route将取决安排程序路径使用什么方法传递#

``` ruby route.rb
namespace :admin do
  post 'tasks/helo' #使用post方式请求
  get 'tasks/say'
end
```

