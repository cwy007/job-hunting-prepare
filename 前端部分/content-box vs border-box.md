# css 属性 box-sizing 里面的 content-box 与 border-box 的差异为何？

通常元素的属性 box-sizing 预设为 content-box，此为保留W3C的标准box model 的行为，其宽高的设定即是内容的宽高，而元素的宽高则是再加上padding以及border。

border-box则是会把元素的宽高计算包括padding以及border。
