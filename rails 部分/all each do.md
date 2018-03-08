我们经常用以下 script 寄送email给所有注册的使用者，但当网站规模增大后，在服务器执行这个脚本时经常会挡掉，该如何解决？
```ruby
User.all.each do |user|
  ...
end
```

# 解答
可以将 User.all.each 替换成 User.where(:conditions => "border_id = 5" ).find_in_batches( :batch_size => 1000), 这样就会每抓一千笔跑一个循环，不会一次抓一百万笔造成机器崩溃。

详细解答：

http://api.rubyonrails.org/classes/ActiveRecord/Batches.html#method-i-find_in_batches


update_all
```ruby
# update_all(updates) Link
# Updates all records in the current relation with details given. This method constructs a single SQL UPDATE statement and sends it straight to the database. It does not instantiate the involved models and it does not trigger Active Record callbacks or validations. However, values passed to update_all will still go through Active Record's normal type casting and serialization.

# Parameters
# updates - A string, array, or hash representing the SET part of an SQL statement.

# Examples
# Update all customers with the given attributes
Customer.update_all wants_email: true

# Update all books with 'Rails' in their title
Book.where('title LIKE ?', '%Rails%').update_all(author: 'David')

# Update all books that match conditions, but limit it to 5 ordered by date
Book.where('title LIKE ?', '%Rails%').order(:created_at).limit(5).update_all(author: 'David')

# Update all invoices and set the number column to its id value.
Invoice.update_all('number = id')
```

find_in_batches
http://api.rubyonrails.org/classes/ActiveRecord/Batches.html#method-i-find_in_batches

transaction
update_column
sneaky-save (gem)

select only need:
Post.select("column1, colum2").where("id < 10")

acts_as_achive(gem)(soft_delete)
