---
layout: post
title: "rails namespace"
date: 2013-09-28 18:17
comments: true
categories: ['rails','namespace','ruby']
---


#关于rails中的namespace
namespace可以将某些控制器集中在一个区域下，从而可以有效地权限管理等操作。

```
rails g controller admin/managers
```

我们可以用以上的命令创建在一个namespace下的控制器`manager`

当然也需要在`route.rb`下配置你的route中的namespace

``` ruby
namespace :admin do
    post 'manager/users'
    get  'manager/pushTasks'
end
```




