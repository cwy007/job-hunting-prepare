# 为什么Rails开发喜欢用CoffeeScript

CoffeeScript 本身也是一种程序语言，开发者可以通过写 coffeescript 编译产生 js。
它的语法有点像 ruby 与 python 的混合。

```coffeescript
name = "Rails";
greeting_words = "Hi, #{name}"
say_hi = (name) ->
  if name
    "Hello, #{name}"
  else
    greeting_words


jQuery ->
  $('#content').focus
```

编译后

```js
var greeting_words, name, say_hi;

name = "Rails";

greeting_words = `Hi, ${name}`;

say_hi = function(name) {
  if (name) {
    return `Hello, ${name}`;
  } else {
    return greeting_words;
  }
};

jQuery(function() {
  return $('#content').focus;
});

```

# js 存在的几种问题：

* js 是 functional language
* 虽然是 oop，但却是 prototype-based
* js 是 dynamic language，更像 lisp而不是 c/Java，但却用了 c/java 的语法
* 名字里面有 Java 但却和 Java 没什么关系
* 明明是 functional / dynamic 语言，更偏向 ruby/python，却使用了 ruby/python 的语法。原本可以是一个很美的语言，却变成了悲剧。

coffee 的诞生就是为了解决这种局面，重新让写 js 变的很美。

# coffee 做的几项努力：
1. 改善语法
js 目前使用的与本身不搭嘎的 c/java 语法，coffee 改用了深受 lisp 影响的 ruby + python 的混合语法。

2. 借鉴其他语言的好处
coffee 从其他语言借鉴了不少好处，写起来更方便

Array ( From Python )
```coffeescript
# Array
list = [1, 2, 3, 4, 5]
# list comprehensions
cubes = (math.cube num for num in list)
# array slicing
copy = list[0...list.length]
# array generators
countdown = (num for num in [10..1])
```

String (From Ruby)
```CoffeeScript
author = "Wittgenstein"
quote  = "A picture is a fact. -- #{ author }"
```

# good parts
coffee 留下了 js 的 good parts，在设计上尽量消除 js 原生特性会产生的缺点。

1. 消除到处污染的全局变量
开发者在写js时，常不自觉地使用全局变量，导致很多污染问题，而通过coffee产生出来的js，变量一律为局部变量（以var开头）

2. protected code
使用coffee写function，产生出来的js必定以一个anonymous function： function(){}();自我包裹，独立运作，不干扰到其他函数。

3. 使用 -> 和 缩排，让写function更不容易出错
在写js时最令人不爽的莫过如 function(){}()；这些复杂的括号，分号一漏，程式就不知道死在哪里了。
coffee产生出来的js，能够确保括号们绝对不会漏掉。

4. 跟容易侦测到语法错误并拦阻
js在语法错误时非常难以侦测，几乎是每一个程序员的噩梦。
而coffee是一门需要编译的语言，可以利用这样的特性挡掉语法错误的机会。

5. 实作面向对象变的简单
js 是一种面向对象的语言，里面所有东西，几乎都是对象。
在js中我们要实作oop有很多种方式，你可以使用prototype，function，或者是object。但不论是哪一种途径，其实都不简单。
但coffee让这件事变简单了

```coffee
class Animal
  constructor: (@name) ->

  move: (meters) ->
    alert @name + " moved #{meters}m."

class Snake extends Animal
  move: ->
    alert "Slithering..."
    super 5

class Horse extends Animal
  move: ->
    alert "Galloping..."
    super 45

sam = new Snake "Sammy the Python"
tom = new Horse "Tommy the Palomino"

sam.move()
tom.move()
```

编译后：
```js
var Animal, Horse, Snake, sam, tom;

Animal = class Animal {
  constructor(name) {
    this.name = name;
  }

  move(meters) {
    return alert(this.name + ` moved ${meters}m.`);
  }

};

Snake = class Snake extends Animal {
  move() {
    alert("Slithering...");
    return super.move(5);
  }

};

Horse = class Horse extends Animal {
  move() {
    alert("Galloping...");
    return super.move(45);
  }

};

sam = new Snake("Sammy the Python");
tom = new Horse("Tommy the Palomino");

sam.move();
tom.move();
```
6. 容易构建 class，也很 Ruby Way

```coffeescript
class Animal
  constructor: (@name) ->
```

7. 易于在class內添加function
```coffeescript
class Animal
  constructor: (@name) ->

  move: (meters) ->
    alert @name + " moved #{meters}m."
```

8. 实作继承
```coffee
class Animal
  constructor: (@name) ->

  move: (meters) ->
    alert @name + " moved #{meters}m."

class Snake extends Animal
  move: ->
    alert "Slithering..."
    super 5
```

9. 更容易写测试
因为实作面向对象非常容易，所以写测试这件事也更加容易了。
所以不少node.js套件或者js的library后来都该用coffeescript来写。


# 参考链接

https://rocodev.gitbooks.io/rails-102/content/chapter1-mvc/a/coffeescript.html

http://coffeescript.org/#top

http://coffeescript.org/#try
