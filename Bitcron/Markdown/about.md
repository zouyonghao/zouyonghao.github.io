---
title: 关于 Markdown
date: 2016-07-27 21:51:12
Tags: About, Markdown
---

> Markdown 会被解释为一种 **“标记语法”**，实际上，可以不用去理解这种看似晦涩的意思。
> Markdown 接近于普通文本，另外再由少数几个语法规则描述文本结构的一种约定方式；而且花很少的时间，就能很容易掌握的技巧。
> 换一种说法，Markdown 是给**专注于“偷懒”**，却不牺牲最终产出的人群使用的。

## 基本语法

###  标题
```
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```
分别对应HTML中的`<h1>一级标题</h1>`，以此类推。

`**用两个星号标记起来，表示加粗**`，`*一个星号，表示斜体*`，`~~这样子表示删除~~`，这些就是最基本的语法了。


## 插入链接
**插入链接:**
这是一个 `[链接](http://url.com/)`

**快速链接:**
只需要在网址头尾用尖括号包裹即可，比如`<http://url.com>`

**特别支持:**
`[Google (target=_blank id=google_link)](google.com)`  其中内容括号内的`target=_blank id=google_link` 会自动扩展到最终 HTML 对应 A 标签下的属性，另外，`google.com` 作为一个域名，不需要补全`http://`, 最终会自动补全。


## 插入图片
跟插入链接的方式很像，就是前面多一个`!`， 但是在一般的客户端编辑器，比如 [MarkEditor](http://markeditor.com) 中直接拖入图片就可以。
`![)](图片的url)`


## 列表

**无序列表:**
```
-   Red
-   Green
-   Blue
```
**有序列表则使用数字接着一个英文句点：**
```
1.  Bird
2.  McHale
3.  Parish
```


## 居中与居右
单独一行的时候，`[文本内容]`表示居中对齐，`[文本内容]]`表示居右(右侧再多一个`]`)，其它默认情况下都是居左。


## 内容引用
用`>`放在段首，之后是空格，输入文字:

```
> 你
> 一会看我
> 一会看云
```



## 分割线
**`-`加上空格组成，三个以上:**
```
- - - - - -
```