# 参考链接
https://rocodev.gitbooks.io/rails-102/content/chapter2-rails/restful.html

# 什么是 RESTful
representational state transfer 简称 REST
一种软件架构风格，由于比较简介，各大主流网站的 API 都以采用此种风格进行设计

REST 提出的一些概念和准则：
1. 网络上的所有事物都将被抽象为资源 resource
2. 每个资源对应一个唯一的资源标识 resource identifier        （uri)
3. 通过通用的介面 generic connector interface 对资源进行操作 （http）
4. 对资源的各种操作不会改变资源的标识 resource identifier
5. 所有的操作都是无状态的 stateless

RESTful web services：
使用 HTTP 并且遵守 REST 设计原则的协议

HTTP 请求方法：
GET
一组资源 URI
http://example.com/resources
使用给定的一组资源，替换当前的整组资源
单个资源 URI
http://example.com/resources/26
获取指定资源的详细信息，格式可以自选一个合适的 media type （eg：xml， json）

POST
http://example.com/resources
在一组资源中追加新的元素，通常返回单个资源的 URL
http://example.com/resources/26
把指定资源当作一个资源组，并在其下追加新的元素，使其隶属于当前资源

PUT / PATCH
http://example.com/resources
列出URI，以及该资源组中每个资源的详细信息（后者可选）
http://example.com/resources/26
替换指定的资源，将其追加到对应的资源组中

DELETE
http://example.com/resources
删除整组资源
http://example.com/resources/26
删除指定资源

维护性：解决程序码上的风格不一

介面统一：action as resource
resource 指的是 data + representation（表现形式 html，json，xml）
Rails 透过 responder 的设计，让一个action可以以文件扩展名(.json, .xml, .csv ...)的形式，提供不同的representation

开发速度：透过CRUD七个action + HTTP 5 个动词 + 表单 helper 与 URL helper实现高速开发

# 请手写 CRUD 七个 action

```ruby
class PostsController < ApplicationController
  before_action :set_post, only: [:show, :edit, :update, :destroy]

  # GET /posts
  # GET /posts.json
  def index
    @posts = Post.all
  end

  # GET /posts/1
  # GET /posts/1.json
  def show
  end

  # GET /posts/new
  def new
    @post = Post.new
  end

  # GET /posts/1/edit
  def edit
  end

  # POST /posts
  # POST /posts.json
  def create
    @post = Post.new(post_params)

    respond_to do |format|
      if @post.save
        format.html { redirect_to @post, notice: "Post was successfully created." }
        format.json { render :show, status: :created, location: @post }
      else
        format.html { render :new }
        format.json { render json: @post.errors, status: :unprocessable_entity }
      end
    end
  end

  # PATCH/PUT /posts/1
  # PATCH/PUT /posts/1.json
  def update
    respond_to do |format|
      if @post.update
        format.html { redirect_to @post, notice: "Post was successfully updated." }
        format.json { render :show, status: "ok", location: @post }
      else
        format.html { render :edit }
        format.json { render json: @post.errors, status: :unprocessable_entity }
      end
    end
  end

  # DELETE /posts/1
  # DELETE /posts/1.json
  def destroy
    @post.destroy
    respond_to do |format|
      format.html { redirect_to posts_url, notice: "Post was successfully destroyed." }
      format.json { head: :no_content }
    end
  end

  private

    def set_post
      @post = Post.find(params[:id])
    end

    def post_params
      params.require(:post).permit(:title, :body)
    end
end
```
