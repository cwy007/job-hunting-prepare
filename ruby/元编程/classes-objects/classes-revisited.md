# 类自身也是对象

* 类和其他对象一样，也有自己的类 Class
```ruby
2.4.2 :031 > String.class
 => Class
```
* 有自己的方法
一个对象的方法也是其类的实例方法
一个类的方法就是Class类的实例方法

* 有自己的变量

class vs superclass
```ruby
2.4.2 :043 > String.superclass
 => Object
2.4.2 :044 > String.superclass.superclass
 => BasicObject
2.4.2 :045 > String.superclass.superclass.superclass
 => nil
2.4.2 :046 > String.class
 => Class
2.4.2 :047 > String.class.class
 => Class
```

```shell
2.4.2 :050 > class Str < String
2.4.2 :051?>   end
 => nil
2.4.2 :052 > ss = Str.new
 => ""
2.4.2 :053 > ss.class
 => Str # 对象 ss 自身的类
2.4.2 :054 > Str.class
 => Class # 类 Str 也是对象，他自身的类为 Class
2.4.2 :055 > Str.superclass
 => String # 类的超类superclass为该类所继承的类
2.4.2 :056 >
```

# 一个类只不过是一个增强的 Module，增加了三个方法而已
Class#new，Class#superclass，Class#allocate
```shell
2.4.2 :057 > Class.superclass
 => Module
2.4.2 :058 > Class.superclass.superclass
 => Object
2.4.2 :059 > Class.superclass.superclass.superclass
 => BasicObject
2.4.2 :060 > Class.superclass.superclass.superclass.superclass
 => nil
2.4.2 :061 > Class.instance_methods(false)
 => [:new, :allocate, :superclass]
```

类和模块基本上是一样的。

Ruby 对象体系的根结点 BasicObject。

module基本上就是一组实例方法，而类是增加了若干新功能的模块。

# 清晰性
希望它在别处被include时，选用module。
希望他被实例化或继承时，使用类。

明确表明你的意图。
