---
layout: post
title: "Rails little note 1"
date: 2013-06-17 16:26
comments: true
categories: [Rails, ruby]
---

##rails cli##
Active Record 支持的数据类型
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

###rails migration###

Migration 是继承 ActiveRecord::Migration 的一个子类，它实现了两个方法： up (执行需要的改变)和 down (恢复所做的改变)
Active Record 提供以下独立于数据库的方法，用来执行普通数据定义任务的方法:
* add_colmn
* add_index
* change_column
* change_table
* create_table
* create_join_table
* drop_table
* remove_column
* remove_index
* rename_column

```ruby ruby 创建一个migration
rails generate migration MIGRATION_NAME
```
使用up/down方法
Migration里面的down方法能复原up方法所造成的变更。也就是说如果执行了up然后 再执行down，那么数据库的schema应该会没有改变。所以说，如果用up建立一个数据表， 就应该在down方法中删除它。明智的做法会使用跟up完全相反的顺便来做这些事情。

回滚（Rolling Back）
另一个常见的任务是回滚最后一个版本。比如你不小心打错了要修正。输入回滚命令时可以 不用输入先前版本的版本号，直接这样就行了：

``` bash
$ rake db:rollback
```
这样会执行最后一个migration的down方法。如果要恢复多个migrations的话，可以多给 一个STEP参数：

``` bash
$ rake db:rollback STEP=3
```
这样会执行最后3个migrations的down方法。

要回滚然后重新执行最后一个migration的话可以直接执行db:migrate:redo。如果要回滚 重新执行的不止一个版本时可以用STEP参数，就跟db:rollback的用法一样：

``` bash
$ rake db:migrate:redo STEP=3
```
这两个rake任务只是用起来比较方便，让你可以不用输入一大串版本号数字。除了输入比较 方便外没有比db:migrate多做什么额外的工作。

4.2 重置数据库
最后是db:reset任务，它会删除数据库，然后重新建立数据库并在重新建立的数据库中 载入当前的schema。

所谓的载入schema跟执行全部的migrations是不一样的，请参照： schema.rb 。

4.3 执行指定的migration
如果你需要执行一个指定的migration的up或down方法，那么你可以用db:migrate:up和 db:migrate:down这两个任务。你只需指定版本号，就可以触发它的up或down方法：
``` bash
$ rake db:migrate:up VERSION=20080906120000
```
以上会执行20080906120000这个版本的migration的up方法。它会去确认这个migration之前有 没有跑过，所以，如果Active Record认为20080906120000已经跑过，那么执行 db:migrate:up VERSION=20080906120000将不会做任何操作。

###rails 删除控制器###
``` ruby
rails destroy
```


