# 1请问如果一个 div 里面所有的子元素都有 float: left 这个属性时，这个 div 会发生什么情况？要如何解？

div 里面有 浮动元素时，会造成外层的 div 元素不会跟子元素的高度一起变动。
解决此问题，可以在外层div加上 overflow:auto;


http://xyz.cinc.biz/2015/11/div-float-auto-height.html
