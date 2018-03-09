# 方法查找
* 接受者 receiver
被调用方法所在的对象

* 祖先链 ancestors chain

Object 所有类的默认超类
BasicObject ruby 类体系结构的根结点

为了查找一个方法，ruby首先在接受者的类中查找，然后一层一层在祖先链中查找，直到找到这个方法为止。

祖先链是从类到其超类

# 画图顺序
“向右一步，再向上”

当你在一个类中包含一个module时，ruby刷了些小花招。
ruby建了一个封装该模块的匿名类，并把这个匿名类插入到祖先链中，其在链中的位置正好包在它的类上方。


“封装” wrapper 类，叫做包含include类，又时也叫代理proxy类

有很多模块的复杂类体系结构

# kernel module
Object 类包含了 Kernel 模块，因此Kernel就进入到每个对象的祖先链
这样在每个对象中可以随意调用Kernel模块的方法

如果给这个Kernel模块增加一个方法，这个内核方法Kernel method就对所有的对象可用

# RubyGems 是ruby的包管理器
gem() 用来激活给定版本的gem
