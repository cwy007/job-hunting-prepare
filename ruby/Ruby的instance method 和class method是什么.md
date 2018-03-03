# 参考链接
https://rocodev.gitbooks.io/rails-102/content/chapter3-ruby/instance_method_class_method.html

# Ruby 的 instance method / class method 是什么?

instance method：就是给 class 的实例呼叫的方法。
class method：就是给 class 层呼叫的方法。

举例说明，假设我们有一个 class Test 长这样：

```ruby
class Test
# 在 class 內定义 method 时，加上 self 表示要直接取用 class
  def self.class_method
      "class method"
  end

  def instance_method
      "instance method"
  end
end
```

呼叫 class method 时的情况：

```ruby
#class的呼叫
Test.class_method # => "class method"
Test.instance_method # => NoMethodError: undefined method `instance_method' for Test:Class
```

呼叫 instance method 时的情况：

```ruby
#class 实例的呼叫
test = Test.new  # => #<Test:0x007fd103969840>
test.class_method # => undefined method `class_method' for #<Test:0x007fd103969840>
test.instance_method # => "instance method"
```
