# 如果有需要时间的功能如下：
使用者确认购买某商品后，需要在下一个页面秀出成功购买的讯息，此外还要发email给使用者，你会这么实作？

我们可以在使用者submit送出订单后，经由model运算完，导向成功购买的页面，并同时显示购买的资讯，然后可以在model里面实作一个发送使用者email的method，并使用after_create 在购买完成后，触发执行发送email 的行为。
