# css基本语法及页面引用

## css基本语法

css的定义方法是：

选择器 { 属性:值; 属性:值; 属性:值;}

选择器是将样式和页面元素关联起来的名称，属性是希望设置的样式属性每个属性有一个或多个值。代码示例：

	div{ width:100px; height:100px; color:red }

## css页面引入方法：

1、外联式：通过link标签，链接到外部样式表到页面中。

	<link rel="stylesheet" type="text/css" href="css/main.css">

2、嵌入式：通过style标签，在网页上创建嵌入的样式表。

    <style type="text/css">
        div{ width:100px; height:100px; color:red }
        ......
    </style>

3、内联式：通过标签的style属性，在标签上直接写样式。

	<div style="width:100px; height:100px; color:red ">......</div>