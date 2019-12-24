---
layout:     post                   
title:      Liquid模板语言（2）
subtitle:   Liquid 标记介绍 
date:       2019-12-24
categories: 学习笔记
author:     Leo Zhao
header-img: 
catalog: true                       # 是否归档
tags:                               #标签

    - Liquid
excerpt: Liquid末班语言的基本简介，从官网扒过来做查询资料的。 
mathjax: true
---

# Liquid Tags



[TOC]


# 注释

`comment` 标记让你能够在 Liquid 模板中书写的内容不被输出。任何书写在 `comment` 起始与结束标记之间的内容都不会被输出，如果是 Liquid 代码则不会被执行。

输入

```
Anything you put between {% comment %} and {% endcomment %} tags
is turned into a comment.
```

输出

```
Anything you put between  tags
is turned into a comment.
```


# 控制流

控制流标记（control flow tag）能够根据编程逻辑改变 Liquid 输出的信息。

## if

只有当某个条件为 `true` 时才执行一段代码。

输入

```
{% if product.title == 'Awesome Shoes' %}
  These shoes are awesome!
{% endif %}
```

输出

```
These shoes are awesome!
```

## unless

与 `if` 相对 – 只有当某个条件**不**成立时才执行一段代码。

输入

```
{% unless product.title == 'Awesome Shoes' %}
  These shoes are not awesome.
{% endunless %}
```

输出

```
These shoes are not awesome.
```

和如下实例的执行结果一致：

```
{% if product.title != 'Awesome Shoes' %}
  These shoes are not awesome.
{% endif %}
```

## elsif / else

为 `if` 或 `unless` 添加更多状态判断。

输入

```
<!-- If customer.name = 'anonymous' -->
{% if customer.name == 'kevin' %}
  Hey Kevin!
{% elsif customer.name == 'anonymous' %}
  Hey Anonymous!
{% else %}
  Hi Stranger!
{% endif %}
```

输出

```
Hey Anonymous!
```

## case/when

创建一个开关表达式，用于将一个变量和多个不同值进行比较。`case` 用于初始化一个开关表达式，`when` 用于比较他们的值。

输入

```
{% assign handle = 'cake' %}
{% case handle %}
  {% when 'cake' %}
     This is a cake
  {% when 'cookie' %}
     This is a cookie
  {% else %}
     This is not a cake nor a cookie
{% endcase %}
```

输出

```
This is a cake
```



# 迭代／循环

迭代（或循环）标记（iteration tag）用于重复运行一段代码。

## for

重复运行一段代码。`for` 循环中所能够使用的属性请参考 [forloop (object)](https://docs.shopify.com/themes/liquid/objects/for-loops)。

输入

```
  {% for product in collection.products %}
    {{ product.title }}
  {% endfor %}
```

输出

```
hat shirt pants
```

### break

循环过程中若干遇到 `break` 标记（tag）即停止循环。

输入

```
{% for i in (1..5) %}
  {% if i == 4 %}
    {% break %}
  {% else %}
    {{ i }}
  {% endif %}
{% endfor %}
```

输出

```
1 2 3
```

### continue

循环过程中若遇到 `continue` 标记（tag）则跳出当前循环。

输入

```
{% for i in (1..5) %}
  {% if i == 4 %}
    {% continue %}
  {% else %}
    {{ i }}
  {% endif %}
{% endfor %}
```

输出

```
1 2 3   5
```

## for (parameters)

### limit

限定循环执行的次数。

输入

```
<!-- if array = [1,2,3,4,5,6] -->
{% for item in array limit:2 %}
  {{ item }}
{% endfor %}
```

输出

```
1 2
```

### offset

从指定索引号开始执行循环。

输入

```
<!-- if array = [1,2,3,4,5,6] -->
{% for item in array offset:2 %}
  {{ item }}
{% endfor %}
```

输出

```
3 4 5 6
```

### range

定义循环执行的范围。可利用数字或变量来定义此执行范围。

输入

```
{% for i in (3..5) %}
  {{ i }}
{% endfor %}

{% assign num = 4 %}
{% for i in (1..num) %}
  {{ i }}
{% endfor %}
```

输出

```
3 4 5
1 2 3 4
```

### reversed

反转循环的执行顺序。注意和 `reverse` 过滤器（filter）的拼写是不同的。

输入

```
<!-- if array = [1,2,3,4,5,6] -->
{% for item in array reversed %}
  {{ item }}
{% endfor %}
```

输出

```
6 5 4 3 2 1
```

## cycle

循环一组字符串并按照它们传入的顺序将其输出。每次调用 `cycle` 时，传入的参数中的下一个字符串将被输出。

`cycle` 必须用在 [for](https://liquid.bootcss.com/tags/iteration/#for) 循环中。

输入

```
{% cycle 'one', 'two', 'three' %}
{% cycle 'one', 'two', 'three' %}
{% cycle 'one', 'two', 'three' %}
{% cycle 'one', 'two', 'three' %}
```

输出

```
one
two
three
one
```

`cycle` 的使用场景包括：

- 对表格中的奇数／偶数行输出相应的类（class）
- 在一行中的最后一列输出一个唯一的类（class）

## cycle (parameters)

`cycle` 能够接受一个叫做 `cycle group` 的参数，以便满足你在模版中需要使用多个 `cycle` 代码块的情况。如果没有为 cycle group 命名，那么将会假定带有相同参数的 cycle 调用属于同一个组（group）。

## tablerow

生成一个 HTML 表格。必须用 `` 和 `` 这两个 HTML 标签将其包裹起来。

输入

```
<table>
{% tablerow product in collection.products %}
  {{ product.title }}
{% endtablerow %}
</table>
```

输出

```
<table>
  <tr class="row1">
    <td class="col1">
      Cool Shirt
    </td>
    <td class="col2">
      Alien Poster
    </td>
    <td class="col3">
      Batman Poster
    </td>
    <td class="col4">
      Bullseye Shirt
    </td>
    <td class="col5">
      Another Classic Vinyl
    </td>
    <td class="col6">
      Awesome Jeans
    </td>
  </tr>
</table>
```

## tablerow (parameters)

### cols

定义表格应当有多少列。

输入

```
{% tablerow product in collection.products cols:2 %}
  {{ product.title }}
{% endtablerow %}
```

输出

```
<table>
  <tr class="row1">
    <td class="col1">
      Cool Shirt
    </td>
    <td class="col2">
      Alien Poster
    </td>
  </tr>
  <tr class="row2">
    <td class="col1">
      Batman Poster
    </td>
    <td class="col2">
      Bullseye Shirt
    </td>
  </tr>
  <tr class="row3">
    <td class="col1">
      Another Classic Vinyl
    </td>
    <td class="col2">
      Awesome Jeans
    </td>
  </tr>
</table>
```

#### limit

在执行到指定的脚标（index）之后退出 tablerow 。

```
{% tablerow product in collection.products cols:2 limit:3 %}
  {{ product.title }}
{% endtablerow %}
```

### offset

在指定的脚标（index）之后开始执行 tablerow 。

```
{% tablerow product in collection.products cols:2 offset:3 %}
  {{ product.title }}
{% endtablerow %}
```

### range

定义循环执行的范围。可利用数字和变量来定义执行范围。

```
<!--variable number example-->

{% assign num = 4 %}
<table>
{% tablerow i in (1..num) %}
  {{ i }}
{% endtablerow %}
</table>

<!--literal number example-->

<table>
{% tablerow i in (3..5) %}
  {{ i }}
{% endtablerow %}
</table>
```



# 原始内容

`raw` 标记临时禁止处理其所包围的代码。如果输出的内容与 Liquid 模板语言有冲突时（例如 Mustache、Handlebars 模板语言）可以避免冲突。

输入

```
{% raw %}
  In Handlebars, {{ this }} will be HTML-escaped, but
  {{{ that }}} will not.
{% endraw %}
```

输出

```
In Handlebars, {{ this }} will be HTML-escaped, but {{{ that }}} will not.
```



# 变量

变量标记（variable tag）用于创建新的 Liquid 变量。

## assign

创建一个新变量。

输入

```
{% assign my_variable = false %}
{% if my_variable != true %}
  This statement is valid.
{% endif %}
```

输出

```
  This statement is valid.
```

将变量用 `"` 包裹之后则将其当做字符串对待。

输入

```
{% assign foo = "bar" %}
{{ foo }}
```

输出

```
bar
```

## capture

将 `capture` 开始与结束标记之间的字符串捕获之后赋值给一个变量。通过 `{% capture %}` 创建的变量都是字符串。

输入

```
{% capture my_variable %}I am being captured.{% endcapture %}
{{ my_variable }}
```

输出

```
I am being captured.
```

使用 `capture` 时，你还可以利用 `assign` 创建的其他变量创造一个复杂的字符串。

输入

```
{% assign favorite_food = 'pizza' %}
{% assign age = 35 %}

{% capture about_me %}
I am {{ age }} and my favorite food is {{ favorite_food }}.
{% endcapture %}

{{ about_me }}
```

输出

```
I am 35 and my favourite food is pizza.
```

## increment

创建一个全新的数值变量，并且在后续每次调用时将此变量的值加 1。初始值是 0。

输入

```
{% increment my_counter %}
{% increment my_counter %}
{% increment my_counter %}
```

输出

```
0
1
2
```

通过 `increment` 标记（tag）创建的变量与通过 `assign` 或 `capture` 创建的变量是相互独立的。

在下面的实例中，名为 “var” 的变量是通过 `assign` 创建的。然后将 `increment` 标记（tag）在相同的变量名上应用了几次。注意，`increment` 标记（tag）不会对 `assign` 创建的变量 “var” 及其值产生任何影响。

输入

```
{% assign var = 10 %}
{% increment var %}
{% increment var %}
{% increment var %}
{{ var }}
```

输出

```
0
1
2
10
```

## decrement

创建一个全新的数值变量，并且在后续每次调用时将此变量的值减 1。初始值是 -1。

输入

```
{% decrement variable %}
{% decrement variable %}
{% decrement variable %}
```

输出

```
-1
-2
-3
```

和 [increment](https://liquid.bootcss.com/tags/variable/#increment) 类似，在 `decrement` 之中创建的变量与通过 `assign` 或 `capture` 创建的变量是互相独立的。