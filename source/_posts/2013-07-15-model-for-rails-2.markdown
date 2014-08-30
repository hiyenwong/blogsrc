---
layout: post
title: "Model-for-rails(2)"
date: 2013-07-15 15:08
comments: true
categories: [Rails,ruby,model,migration]
---



#Migeration#
Migeration是一种可以随时改变数据模式的一种途径。通过使用Ruby DSL,从而摆脱了SQL的编写，从而使得数据库独立。Migeration保存着你历史数据结构，ActiveRecord会通过更新`db/schema.rb`来同步更新你的数据库结构。

##创建一个标准的Migration##
使用`rails g migration MIGRATION_NAME`用来创建一个标准的空migration.
* 如果你的migration名字是'AddXXXToyyy'或是'RemoveXXXToYYY',那么migration会自动在文档里创建`add_column`或是`remove_column`
* 如果你的migration名字是'CreateXXX'那么他将自动在文档里创建`create_table XXX`

同样如果你的名字是AddXXXRefToYYY,就会自动添加`add_reference :xxx, :yyy, index:true`

如果CreateJoinTableNNNN XXX YYY,则会自动添加`create_join_table :xxx,:yyy`,实际上，他会生成一张表讲带有xxx_id和yyy_id.

另外可以通过`{}`来限制起最大值和多态性比如`$ rails generate migration AddDetailsToProducts price:decimal{5,2} supplier:references{polymorphic}
`
##使用change方法 ##
以下方法支持change

* add_column
* add_index
* add_reference
* add_timestamps
* create_table
* create_join_table
* drop_table (must supply a block)
* drop_join_table (must supply a block)
* remove_timestamps
* rename_column
* rename_index
* remove_reference
* rename_table

##回滚migrations##
每个生成的migration都会根据时间自动生成版本号标签，你可以通过`rake db:migrate VERSION=20080906120000` 来回到所要的版本号，如果你只是要回滚到最后一个版本，则可以`rake db:rollback`,或是在最后第三个版本，则可以`rake db:rollback STEP=3`

##REST DB##
REST数据其实很简单，只要执行`rake db:rest`就可以了
