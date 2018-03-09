Object#methods
查看对象的方法列表

Array#grep
过滤特定模式的方法

obj.methods.grep /^my/
查看obj对象中以my开头的方法

对象内部仅仅包含实它的例变量，以及一个对自身类的引用

对象的唯一标识符
Object#object_id

共享同一个类的对象，也共享同样的方法，因此方法必须存放在类中，而非对象中。

实例变量存在对象中，方法存在类中。

# 自省方法
instance_methods vs methods

```shell
2.4.2 :029 > String.instance_methods == 'abc'.methods
 => true
2.4.2 :030 > String.methods == 'abc'.methods
 => false
2.4.2 :031 >
```
