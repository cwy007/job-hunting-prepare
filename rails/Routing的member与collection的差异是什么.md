# 参考链接
https://rocodev.gitbooks.io/rails-102/content/chapter2-rails/routing.html

# Routing 的 member 与 collection 的差异是什么？
Routing 的概念就像是 10086 的语音提示功能，当你打电话给 10086 时，都会有语音提示问你要办什么业务，然后帮你转接到相应的接线员，然后再由这个接线员完成你申请的业务。

Routing 也是做一样的事情，当你想要到某个页面时（办理业务）时，Routing 就会帮你找到负责这个业务的接线员（Controller Action）然后这个接线员就会帮你办理业务，给你想要的页面（View），大功告成。

```ruby
#指定http verb, url 跟 controller action
get 'products/:id' => 'catalog#view'

# 自动按照 rails 内建的 RESTful 路径判断 controller action
resources :products

#member & collection
resources :products do
# 会产生 products/:id/short，对单个资源进行操作
     member do
        get  'short'
        post 'toggle'
    end
# 会产生 products/sold，对一组资源进行操作
    collection do
        get 'sold'
    end
end
```
