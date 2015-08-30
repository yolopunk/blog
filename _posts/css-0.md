title: 对CSS伪类中[:first-child]和[:last-child]的理解
date: 2015-08-03 16:50:41
tags: CSS
---
今天在使用CSS中:first-child和:last-child时遇到了一个奇葩的问题，故记录之以填坑。

首先来个定义：The :last-child CSS pseudo-class represents any element that is the last child element of its parent.
(吐槽一下，W3上的中文定义真的是看不懂！！！)

直接摆例子：
```html
<div class="test">1</div>
<div class="test">2</div>
<div class="test">3</div>
```
在css中可以使用``.loop:first-child``或``.loop:last-child``给第一层或最后一层单独定义样式。

出现问题的情况：
```html
<div class="test">1</div>
<div class="test">2</div>
<div class="test">3</div>
<div>我是大忽悠</div>
```
此时，``.loop:last-child``就会失效，不会作用于任何div。同理，如果在前面加一个div，那么``.loop:first-child``也会失效。

解决方案：
使用一个标签将所有的``.loop``包裹起来，使其有parent，血统很重要啊，不要掺进不相干的子嗣，例如：
```html
<div>
  <div class="test">1</div>
  <div class="test">2</div>
  <div class="test">3</div>
</div>
<div>他们看孙子兵法了。。。</div>
```
这样，``.loop:last-child``就有效了。``.loop:first-child``同理

**总结**

在实际的开发中，DOM结构复杂，当使用到``:first-child``或``:last-child``时，一定要注意，当不起作用时，查看是否将整个层包裹起来了。

（再次吐槽：不要问why，CSS在我看来本身就不严谨，解决问题就好，不要在意这些细节！）
