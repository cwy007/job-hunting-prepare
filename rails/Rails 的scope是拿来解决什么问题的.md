# Rails 的 scope 是拿来解决什么问题的

scope 的作用就是将经常使用或复杂的 ORM (对象关系映射) 语法组合成懒人包，
这样下次在用的时候，只要把懒人包拿出来就可以了。

```Ruby
class Topic < ApplicationRecord
  scope :recent, -> { order("created_at DESC") }
end
```

上面的code我们第一了recent这个scope，以后我们只要下 recent 这个指令就等于下 order("created_at DESC") 是一样的。如此一来就可以让程序更简洁。

使用情景：
* 当有过于复杂的资料查询
* 当有重复使用的资料查询

使用方式
* 不带参数

```ruby
class Post < ApplicationRecord
  scope :published, -> { where(published: true) }
end
```

* 带参数的方式

```ruby
class Post < ApplicationRecord
  scope :created_before, ->(time) { where("created_at < ?", time) }
end
```

* 可以串接在一起，顺序没有影响

```ruby
class Post < ApplicationRecord
  scope :published, -> { where(published: true) }
  scope :created_before, ->(time) { where("created_at < ?", time) }
end

Post.published.created_before(Time.now)
```
