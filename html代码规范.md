# HTML规范

#### 一、属性名命名规范

#### id

​    命名全部用英文单词，不得使用拼音，而且两个单词之间使用 **”-“**，且唯一性`全文其他命名不得与之相同`。

#### class

​	命名全部用英文单词，不得使用拼音，而且两个单词之间使用**”-“**，不得以属性值作为名字。

#### 自定义属性

​	命名属性名以data-属性名命名。

【注】命名要能见名之意，但尽可能的短

~~~html
<div id="nav-container">
    <ul class="nav-lis">
        <li data-btn="index"></li>
    </ul>
</div>
~~~

#### 二、标签

全部使用小写，多使用语义化标签。

子标签应缩进4个空格，除了**window系统**下面进行编写代码可以使用tab键

##### [建议]所有标记都要有结束标签

~~~html
<!--双标记-->
<div></div>
<!--单标记-->
<img/>

~~~

##### [建议]内部属性值不可少，而且a标记的**href**没有跳转使用**javascript:;**,如需跳转顶部，则使用“#”

~~~html
<img src= "图片路径" title= "logo" alt= "这是一张公司标识图" />
<!--点击a标记没有效果-->
<a href= "javascript:;"></a>
<!--跳转至顶部-->
<a href= "#"></a>
~~~

##### [建议]引入 `CSS` 时必须指明 `rel="stylesheet"`。

示例：

```
<link rel="stylesheet" href="page.css">
```

##### [建议] 引入 `CSS` 和 `JavaScript` 时无须指明 `type` 属性。

解释：

`text/css` 和 `text/javascript` 是 `type` 的默认值。

##### [建议] 展现定义放置于外部 `CSS` 中，行为定义放置于外部 `JavaScript` 中。

解释：

结构-样式-行为的代码分离，对于提高代码的可阅读性和维护性都有好处。

##### [建议] 在 `head` 中引入页面需要的所有 `CSS` 资源。

解释：

在页面渲染的过程中，新的CSS可能导致元素的样式重新计算和绘制，页面闪烁。

##### [建议] `JavaScript` 应当放在页面末尾，或采用异步加载。

解释：

将 `script` 放在页面中间将阻断页面的渲染。出于性能方面的考虑，如非必要，请遵守此条建议。

示例：

```
<body>
    <!-- a lot of elements -->
    <script src="init-behavior.js"></script>
</body>
```

##### [建议] 移动环境或只针对现代浏览器设计的 Web 应用，如果引用外部资源的 `URL` 协议部分与页面相同，建议省略协议前缀。

解释：

使用 `protocol-relative URL` 引入 CSS，在 `IE7/8` 下，会发两次请求。是否使用 `protocol-relative URL` 应充分考虑页面针对的环境。

示例：

```
<script src="//s1.bdstatic.com/cache/static/jquery-1.10.2.min_f2fb5194.js"></script>
```

##### [强制] 页面必须使用精简形式，明确指定字符编码。指定字符编码的 `meta` 必须是 `head` 的第一个直接子元素。

解释：

见 [HTML5 Charset能用吗](http://www.qianduan.net/html5-charset-can-it.html) 一文。

示例：

```
<html>
    <head>
        <meta charset="UTF-8">
        ......
    </head>
    <body>
        ......
    </body>
</html>
```

##### [建议] `HTML` 文件使用无 `BOM` 的 `UTF-8` 编码。

## 三、模板中的 HTML

[建议] 模板代码的缩进优先保证 HTML 代码的缩进规则。

示例：

```
<!-- good -->
{if $display == true}
<div>
    <ul>
    {foreach $item_list as $item}
        <li>{$item.name}<li>
    {/foreach}
    </ul>
</div>
{/if}

<!-- bad -->
{if $display == true}
    <div>
        <ul>
    {foreach $item_list as $item}
        <li>{$item.name}<li>
    {/foreach}
        </ul>
    </div>
{/if}
```

##### [建议] 模板代码应以保证 HTML 单个标签语法的正确性为基本原则。

示例：

```
<!-- good -->
<li class="{if $item.type_id == $current_type}focus{/if}">{ $item.type_name }</li>

<!-- bad -->
<li {if $item.type_id == $current_type} class="focus"{/if}>{ $item.type_name }</li>
```

##### [建议] 在循环处理模板数据构造表格时，若要求每行输出固定的个数，建议先将数据分组，之后再循环输出。

示例：

```
<!-- good -->
<table>
    {foreach $item_list as $item_group}
    <tr>
        {foreach $item_group as $item}
        <td>{ $item.name }</td>
        {/foreach}
    <tr>
    {/foreach}
</table>

<!-- bad -->
<table>
<tr>
    {foreach $item_list as $item}
    <td>{ $item.name }</td>
        {if $item@iteration is div by 5}
    </tr>
    <tr>
        {/if}
    {/foreach}
</tr>
</table>
```