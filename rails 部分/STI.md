Rails Guide 對此的說明：
>a way to add inheritance to your models

簡單來講就是讓繼承的 submodel 可以擁有父類別的表格欄位且繼承父類別的方法。

在 Rails 慣例中只要加上type這個欄位在父類別的資料庫中就可以了

例：User有分 Native 跟 Foreigner

```ruby
class User < ActiveRecord::Base
end
class Native < User
end
class Foreigner < User
end
```
這樣就可以了，可以新增 Native User

```ruby
native = Native.create(:name => "foobar")
native.type # => "Native"
```

STI的使用時機是當我們需要一個擁有一樣特性但是不同行為的model時才使用。

https://rocodev.gitbooks.io/rails-102/content/chapter1-mvc/m/sti.html
