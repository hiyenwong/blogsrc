---
layout: post
title: "TDD:spec_helper"
date: 2013-06-18 06:51
comments: true
categories: [TDD,Rails,test,ruby,rspc]
---
Rails 有自带的Test框架，当我们不使用本身框架的时候则在创建controller的时候加入 `--no-test-framework`



## RSpec 生成器 ##
``` ruby
rails g rspec:install
```

## 集成測試 ##
``` bash
$ rails generate integration_test static_pages
```


根據http://railstutorial-china.org/chapter3.html 中例子，在做TDD環節的時候會說找不到visit這個方法，原因並不是你沒有capybara，而是之前你沒有加載,所以需要修改`spec/spec_helper.rb`
``` ruby spec/spec_helper.rb
       require 'capybara/rails'
       require 'capybara/rspec'
       include Capybara::DSL
       .....
       config.include Capybara::DSL
```


