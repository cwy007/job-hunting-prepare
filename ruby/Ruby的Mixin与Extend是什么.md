# Mixin / Extend / Inheritance

在说明 mixin 和 extend 之前，我们必须先了解何为 module？
因为 mixin 与 extend 是在引入 module 时会用到的语法，
而 inheritance 是在继承 class 时会用到的语法。

## Module
module 的好处是：可以选择性的引用 module 内的方法，不会让 module 内的变数或method 与其他 class 互相影响，有点类似 class 补充包的感觉。
而应用 module 的方式就是 mixin 与 extend。

## include vs extend
include 是为了给类的实例添加方法 instance method
extend 是为了添加 class method

```ruby
module Foo
  def foo
    puts 'heyyyyoooo!'
  end
end

class Bar
  include Foo
end

Bar.new.foo # heyyyyoooo!
Bar.foo # NoMethodError: undefined method ‘foo’ for Bar:Class

class Baz
  extend Foo
end

Baz.foo # heyyyyoooo!
Baz.new.foo # NoMethodError: undefined method ‘foo’ for #<Baz:0x1e708>
```

## include 既可以添加 instance method 也可以添加 class method
include 有一个 self.included 钩子，可以用来修改正在including当前module的class，给这个class添加class method

A Common Idiom
Even though include is for adding instance methods, a common idiom you’ll see in Ruby is to use include to append both class and instance methods. The reason for this is that include has a `self.included hook` you can use to modify the class that is including a module and, to my knowledge, extend does not have a hook. It’s highly debatable, but often used so I figured I would mention it. Let’s look at an example.

```ruby
module Foo
  def self.included(base)
    base.extend(ClassMethods)
  end

  module ClassMethods
    def bar
      puts 'class method'
    end
  end

  def foo
    puts 'instance method'
  end
end

class Baz
  include Foo
end

Baz.bar # class method
Baz.new.foo # instance method
Baz.foo # NoMethodError: undefined method ‘foo’ for Baz:Class
Baz.new.bar # NoMethodError: undefined method ‘bar’ for #<Baz:0x1e3d4>
```

# 参考链接
http://www.railstips.org/blog/archives/2009/05/15/include-vs-extend-in-ruby/

https://rocodev.gitbooks.io/rails-102/content/chapter3-ruby/mixin_extend_inheritance.html
