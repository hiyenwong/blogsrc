---
layout: post
title: "model for rails(1)"
date: 2013-07-03 14:20
comments: true
categories: ['rails','model','ruby']
---
#ActiveRecord Models#

我们可以通过`rails g`的命令来创建一个Model
``` bash
rails g model User name:string email:string
```
在`/app/models/`和`/app/db/migration`中会创建相应的文件

##Active Record Basic##
Active Record是一个ORM的框架
###命名规范###
Model/Class|Table/Schema
-----------|------------
Post       |posts
LineItem   |line_items
Deer       |deer
Mouse      |mice
Person     |people

###Schema 模式###
外键 Foreign Keys: tablename_id
主键 Primary Keys: 默认为id

另外还会自动创建两个字段 `created_at` 和`updated_at`


###create or overriding name conventions ###
通常我们继承了一个ActiveRecord的类就好比创建了一张表。
``` ruby Product
class Product < ActiveRecord:Base
end
```
类名通常就是这个表的表名，但其实我们可以重新定义。

``` ruby
changeProduct < ActiveRecord:Base
     self.table_name = "Product"
end
```
手动添加primary_key
``` ruby
set_primary_key "product_id"
```

###about CRUD###






