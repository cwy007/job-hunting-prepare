# 什么时候用 Helper

helper 是一些用在 rails view 当中，用 ruby 产生或整理 html code 的一些小方法。
通常被放在 app/helpers 下，预设的 helper 名称是对应 controller 的。产生controller 时，通常会产生一个同名的 helper。如：PostsController 与 PostsHelper

helper 使用情景：
* 产生的html code 需要与原始程序码进行一些逻辑混合，但又不希望 view 里面搞得太脏。
* 需要与 rails 内建的 helper 交叉使用。

使用helper 封装程序码给专案带来的一些优点：
* Don't repeat yourself。 程序码不重复。
* Good Encapsulation 好的封装性
* 提供 view 模版良好的组织
* 易于修改程序码

```Ruby

module BoardsHelper

# 回传board的name，避免在view中做太多判斷
  def render_board_name(board)
    if board.present?
      board.name
    else
      "unknown"
    end
  end

# 常常重复的区块也可以写进 helper，统一管理
  def render_board_name_path(board)
    link_to(board.name, board_path(board))
  end
end
```

在view中可以直接取用如下

```html
<%= render_board_name_path(@board) %>

```

# 什么时候用 Partial

partial 简单来说就是程序码中的一小段，通常使用在 html 中，使 view 的code 更干净，将重复使用到的区块切成独立的 partial，比如说：页首，页尾，表单，社群插件等，让任何页面都可以读取这段partial，而不用重复写一次一摸一样的 code。

使用情景：
* long template 如果档案html超过两页
* highly duplicated，html 内容高度重复
* independent block，可作为独立的功能区块

```html
<!-- _topic_list.html.erb -->

<ul>
  <% @topics.each do |topic| %>
  <li># <%= topic.id %></li>
  <li>Topic title: <%= link_to topic.title, topic_path %></li>
  <li>Content: <%= topic.content %></li>
  <% end %>
</ul>
```

```html
<%= render "topic_list" %>
```
