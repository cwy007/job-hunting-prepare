# ruby 的常量和文件系统的相似性：
用目录组织文件
用模块组织常量

rake 是ruby流行的构建系统。

```ruby
module Rake
  class Task
  end
end
```

Task 类的全名 Rake::Task
象 Rake 这样，仅仅充当常量容器的模块，称为命名空间。

安全的常量，与别的类库不发生冲突。

常量是嵌套的，可以通过路径模式进行标识。
::
常量前加上双引号表示根路径。

load 方法可以执行代码
require 则是用来导入import类库
