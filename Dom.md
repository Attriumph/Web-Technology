# Dom
# Summary of CSS lecture from CSCI 571 
(refer:http://cs-server.usc.edu:45678/lectures.html)
## 1.What is DOM？

The DOM represents an XML file as a tree
The documentElement is the top-level of the tree.
This element has one or many childNodes that represent the branches of the tree.
to be used with any programming language and any operating system

W3C DOM 标准被分为 3 个不同的部分：

核心 DOM - 针对任何结构化文档的标准模型
XML DOM - 针对 XML 文档的标准模型
HTML DOM - 针对 HTML 文档的标准模型

If you use innerHTML, don't use the += operator with innerHTML for the following reason:

Every time innerHTML is set, the HTML has to be parsed, a DOM constructed, and inserted into the document. This takes time
It's better to just call appendChild:

HTML DOM 是关于如何获取、修改、添加或删除 HTML 元素的标准。


getElementById()	返回带有指定 ID 的元素。
getElementsByTagName()	返回包含带有指定标签名称的所有元素的节点列表（集合/节点数组）。
getElementsByClassName()	返回包含带有指定类名的所有元素的节点列表。
appendChild()	把新的子节点添加到指定节点。
removeChild()	删除子节点。
replaceChild()	替换子节点。
insertBefore()	在指定的子节点前面插入新的子节点。
createAttribute()	创建属性节点。
createElement()	创建元素节点。
createTextNode()	创建文本节点。
getAttribute()	返回指定的属性值。
setAttribute()	把指定属性设置或修改为指定的值。
