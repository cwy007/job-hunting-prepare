# 调用方法时
1. 找到这个方法
向右一步，再向上

2. 执行这个方法
当调用一个方法时，ruby需要持有一个接受者引用，正是由于这个引用的存在，他可以记得那个对象是接受者，再用它来执行这个方法


ruby解释器

# 当前对象
每一行代码都会在一个对象中执行

可以用 self 关键字来表示 当前对象，
也可以用self访问当前对象。

实例变量
没有指明接受者的方法调用
```
2.4.2 :004 > class MyClass
2.4.2 :005?>     def testing_self
2.4.2 :006?>         @var = 10     # An instance variable of self
2.4.2 :007?>         my_method()   # Same as self.my_method()
2.4.2 :008?>         self
2.4.2 :009?>       end
2.4.2 :010?>
2.4.2 :011 >       def my_method
2.4.2 :012?>         @var = @var + 1
2.4.2 :013?>       end
2.4.2 :014?>   end
 => :my_method
2.4.2 :015 >
2.4.2 :016 >   obj = MyClass.new
 => #<MyClass:0x00007fbb5a0e14c0>
2.4.2 :017 > obj.testing_self
 => #<MyClass:0x00007fbb5a0e14c0 @var=11>
```

# 一个对象的组成
<MyClass:0x00007fbb5a0e14c0 @var=11>

MyClass: 类别引用，obj.class
0x00007fbb5a0e14c0：唯一标识, obj.object_id
@var=11: 实例变量
```
2.4.2 :020 > obj.methods.grep(/^inst/)
 => [:instance_of?, :instance_variable_defined?, :instance_variable_set, :instance_variable_get, :instance_variables, :instance_eval, :instance_exec]
2.4.2 :021 > obj.instance_variables
 => [:@var]
```

# 当前那个对象在充当self角色

当开始运行ruby程序时，ruby解释器会创建一个名为main的对象作为当前对象。
这个对象main，又时被称为顶级上下文top level context。
名字由来：因为此时处于调用堆栈的顶层。

此时：
要么没有调用任何方法；
要么调用的方法都已经返回。

# private key word
私有方法服从一个简单的规则：
不能明确指定一个接受者，来调用一个私有方法。
只能调用于隐含的接受者上 -- self上。

私有规则：
1. 如果调用方法的接受者不是你自己，则必须明确指明一个接受者；
2. 私有方法只能被隐含接受者调用。

只能在自身中调用一个私有方法。

无需明确指明接受者来调用继承来的方法。

# 没有明确指定超类时，隐式继承Object类

包含什么模块
继承于什么类

没有明确指定接受者的调用都会作用于 self

隐式调用 Book 类的 ancestors 方法

# wrap up
Class 类是 Module 的子类，一个模块基本上是由一个方法组成的包。
类除了具有模块的特性外，还可以被实例化（通过new（））及被组织为层次结构（通过它的superclass（）方法）
