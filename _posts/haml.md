title: haml
date: 2015-07-28 23:50:41
tags: RoR
---
Haml (HTML Abstraction Markup Language) is a lightweight markup language that is used to describe the XHTML of any web document without the use of traditional inline coding.Haml 的职能是替代那些内嵌代码的page：php | erb | asp 。不过， haml避免了直接coding xhtml到模板，因为它实际上就是一个xhtml的抽象描述，内部使用一些code来生成动态内容

## 特点
1. 空格标识层次嵌套关系
2. 良好的标签格式
3. Don’t repeat yourself
4. 遵循CSS标准
5. 集成了Ruby代码
6. 文件后缀为.haml

## 示例
### ERB模板中可以使用的示例变量在haml中仍可使用
```haml
#content
.title
  / ruby 变量 @title=Ruby
  %h1 = @title
  = link_to 'Home', home_url
```
上面的haml代码会被编译为：

```html
<div id="content">
  <div class="title">
    <h1>Ruby</h1>
    <a href="/">Home</a>
  </div>
</div>
```

## XTML Tags
* **%:** 百分号符号是一行的开始，紧接着一个元素的名字，然后后面跟一个可选的修饰语（见下例），比如一个空格，或一行文本等，就会被渲染到这个元素里成为其内容
```haml
%one
  %two
    %three Hey
```
被编译为：

```html
<one>
  <two>
    <three>Hey</three>
  </two>
</one>
```

* **{}:** 括号内的Ruby hash是用来指名一个元素的属性。它作为一个ruby hash的字面量，局部变量也可以在其中使用。Hash放在被定义好的标签之后，基本上就和Ruby语法一样，看例子：
```haml
%head{ :name => "doc_head" }
  %script{ 'type' => "text/"+"javascript", :src => "javascripts/script_#{2+7}" }
```
被编译为 :
```html
<head name="doc_head">
  <script src="javascripts/script_9" type="text/javascript">
  </script>
</head>
```

* **[]:** 方括号跟在一个标签定义之后，包含一个Ruby 对象，被用来为这个标签设置class和id属性。这个class的值被设置为这个对象的类名（两个单词用下划线形式表示，而不是驼峰表示方法）并且id的值被设置为对象的类名加上这个对象的id，也是下划线连接。因为一个对象的id通常是朦胧的实现细节，这是表现model的实例最有用的元素了
```haml
/ def show
/   @user = CrazyUser.find(15)
/ end
%div[@user]
  %bar[290]/
  Hello!
```
被编译为：
```html
<div class="crazy_user" id="crazy_user_15">
  <bar class="fixnum" id="fixnum_581" />
</div>
```
