# 参考链接
https://rocodev.gitbooks.io/rails-102/content/chapter2-rails/db_migration.html

# Rails 为什么要用 migration 管理 db 栏位
在 Rails 的开发流程中，我们会使用 `rails g model post` 产生所需要的 model 档案。
这个指令会在 `app/model/` 下产生 `post.rb`， 这是 model 档案。
也会在 `db/migrate/` 下产生 `(time_stamp)_create_posts.rb`, 这是连带产生的 db migration 档案。

db migration 档案的格式如下：

```ruby
class CreatePosts < ActiveRecord::Migration[5.1]
  def change
    create_table :posts do |t|
      t.string :title
      t.text :body

      t.timestamps
    end
  end
end
```
Rails 开发者将所需要开设的栏位加入 migration 档案，执行 rake db:migrate 即可完成新增资料库和资料库栏位的新增。

同样的，若要对资料库栏位进行变更，也一样透过migration。
`rails g migration add_user_id_to_posts` 会产生一个空的migration挡，再将所需要的变更写入档案，再次执行 rake db:migrate 即可。

```ruby
class AddUserIdToPosts < ActiveRecord::Migration[5.1]
  def change
    add_column :posts, :user_id, :integer
  end
end
```

# 资料库栏位变更在协同开发以及部署上所造成的问题

why：透过 rake 和 migration 对资料库进行操作。
在传统开发流程中，当一个人开发且为进行到部署阶段时，开发者都不会感觉到有什么问题。

## 问题1: 协同开发中程序码与 db 栏位不一致
若专案陆续加入第二位，第三位开发者，就会陷入很大的麻烦：
没有人知道现在的 db schema 长什么样子。
当 A 决定将post的title改为subject时，仅通过 phpMyAdmin 改变了 db schema，而忘了告诉 B，就将 code push 到版本控制系统。
而 B 不知道这一变更，于是 B 的开发端就烂掉了，这样的事层出不穷。

## 问题2: 没有 automation 和 rollback 机制
若没用使用 db migration 机制，再部署时，开发者必须自己手动输入 SQL 或透过 phpMyAdmin 变更数据库栏位。
而这样的动作，在程序码处于产品production环境，且db schema 差异较大时，是非常危险的：
1. 开发者可能由于手动操作的关系打错字，而使线上程序烂掉
2. 因为差异太大，网站可能有停机时间 downtime
3. 当变更资料库栏位后，之后发现程序其实是有问题，无法轻易恢复刚刚所做的变更。

## 对 database 进行版本控制，流程自动化且可恢复
DB schema 难道是不可能被版本控制的吗？
Rails 解決了这样的难题：db migration 正是因此而诞生的最佳实践 best practices。

透过 db migration 挡，可以记录资料库每一次的栏位变化，並且可以被版本控制。而协同开发者，在 checkout 程序码下来后，看到栏位发生变更，只要执行 rake db:migrate 就可以追上资料库的最新进度。

同时 rake db:migrate 的动作是全自动化的，如果开发端能够执行，在 production 环境上也可以重制。而 db migration 档提供了恢复机制，如果程序吗那边出了问题，导致对应的数据库栏位也要该会去，只要执行 rake db:rollback 就可以恢复到上一次变更前的状态。
