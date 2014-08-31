---
layout: post
title: "关于Rails下的分页数据"
date: 2013-11-29 11:11
comments: true
categories: ['rails','pagination','ruby']
---

#Rails 的分页#
Rails下的分页显示数据的插件有很多，比较常用的是will_paginate，源代码在[mislav的github](http://githubs.com/mislav/will_paginate)上去git clone一下。

##如何使用will_paginate呢？##
使用起来没有太多复杂的东西，只需要将`Post.all`替换成如下就可以
``` ruby Post Controller

# :order 作为排序设置
# :per_page 每页的记录
@posts = Post.paginate(:page => params[:page],:order => 'id DESC', :per_page => 20)
```

然后下面我们就是设置视图了
``` erb index.html.erb

<%= page_entries_info @posts %>

<%=
#      :class          => 'pagination',
#      :previous_label => nil,
#      :next_label     => nil,
#      :inner_window   => 4, # links around the current page
#      :outer_window   => 1, # links around beginning and end
#      :link_separator => ' ', # single space is friendly to spiders and non-graphic browsers
#      :param_name     => :page,
#      :params         => nil,
#      :page_links     => true,
#      :container      => true

#      具体操作will_paginate / lib / will_paginate / view_helpers.rb 下面则有批注
will_paginate @posts, :previous_label => '上一页', :next_label => '下一页', :container => false
%>

```
##关于css

http://mislav.uniqpath.com/will_paginate/?page=2 可以去着网站上下载其分页样式，之后将它放到`assets/stylesheets`下就可以了。

``` erb
<div class='digg_pagination'>
<div class='pag_info'>
<%= page_entries_info @posts %>
</div>
<%= will_paginate @posts :previous_label => '上一页', :next_label => '下一页',:container => false %>
</div>

```

-eof-


