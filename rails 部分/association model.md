# 如果今天有一个 rails的商业 app，他需要让产品有不同的规格，不同的属性。
譬如买一件衣服M号 1000 元，库存10件，S号800元库存5件，你会怎么设计这个product关联的model？请写出这个model的栏位跟关系。

可以产生一个 ProductInfo 的model，并于 product产生关联

```ruby
class Product < ApplicationRecord
  has_many :product_infos
end

class ProductInfo < ApplicationRecord
  belongs_to product
end
```

product_id
size
price
stock 
