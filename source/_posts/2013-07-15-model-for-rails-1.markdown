---
layout: post
title: "model for rails(1)"
date: 2013-07-15 14:20
comments: true
categories: ['Rails','model','ruby']
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

###支持的数据类型####
* :binary
* :boolean
* :date
* :datetime
* :decimal
* :float
* :integer
* :primary_key
* :string
* :text
* :time
* :timestamp

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
####create####
Active Record 对象是用hash来呈现的，使用create方法，将数据保存在数据库中
``` ruby
user=User.create(name: "Dexter", location: "mars")
```
而如果使用new方法，则只是实例化，并不保存数据,如果你要保存数据，则是`user.save`

####read#####
更多的关于read的api，可访问http://api.rubyonrails.org/classes/ActiveRecord/Base.html
下面一些简单的关于read的例子
``` ruby
users=User.all #返回所有的用户信息
user=User.first #返回第一条记录
david=User.find_by_name('David') #返回第一条叫David的记录

#按照条件和时间排序搜索
users = User.where(name: 'David', occupation: 'Code Artist').order('created_at DESC')
```
####update####
基本和create性质一样
``` ruby
user=User.find_by_[KEY_NAME]('davis') #KEYNAME所查询的字段名称
user.update(KEYNAME: 'dav') #更新keyname里的值
```

若你要更新所有的值，那update_all会很有用

``` ruby
User.update_all "max_login_attempts = 3, must_change_password = 'true'"
```

####delete####
``` ruby
user = User.find_by_name('David')
user.destroy
```

