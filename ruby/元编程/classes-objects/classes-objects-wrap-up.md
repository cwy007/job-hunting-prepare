# 什么是对象
一组实例变量外加指向其类的引用。
对象的方法并不存在于对象本身，而是存在于对象的类中。
在类中这些方法被称为实例方法。

# 什么是类
类无非就是一个对象（Class 类的一个实例），外加一组实例方法和一个对其超类的引用。
Class类是Module类的子类，因此一个类也是一个模块。

和其他对象一样，类必须通过引用来访问。
你已经使用常量引用过他们：这就是类的名称。

require 引用

对已有的类做一个无意义的猴子补丁。

单元测试

```ruby
module Bookworm
  class Text
  end
end
```

所有的类都是 Class 类的实例

在ruby这样的动态语言中，每个对象都有自己的一组实例变量，它们与其他对象之间是完全独立的--哪怕是同一个类的对象。
