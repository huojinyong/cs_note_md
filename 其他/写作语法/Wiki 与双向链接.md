---
title: Wiki 与双向链接
date: 2021-04-27 13:30
---
## 什么是双向链接？
当使用 `[Title](a_markdown_filepath.md)` 的链接语法引入一篇文档，或者 `[[a_markdown_filepath.md | Title]]` 这个 Wiki 风格的，就会在两个文章之间创建关联。
此时，我们可以查看：当前文档引用了哪些文档 （快捷键为 Command+G）、当前文档被哪些文档引用了（快捷键为 Shift+Command+G），这就是 Metion 内的双向链接机制。

## Wiki 风格的链接语法
### 基础语法
使用 `[[ ]]`  包裹文档的路径名就可以了，如果是以 `.md` 为后缀的，默认可以省略后缀，效果是一样的。
```
[[ a_markdown_filepath ]]
[[ a_markdown_filepath.md ]]
[[ a_markdown_filepath.txt ]]
```

### 路径 + 显示标题
使用 ` | ` 进行分割，这样一来，引入的路径和最终 Markdown 渲染后显示的文本可以不一样。
```
[[ a_markdown_filepath.md | 我是实际显示的链接文本 ]]
```

### 路径 + 显示标题 + 锚点
使用 `#` 进行分割，可以指定锚点到对应文章的某个 Header（层级标题） 上，这个指定的锚点 key 应该是英文的。

下面的语法都是可以的：
```
[[ a_markdown_filepath.md | 我是实际显示的链接文本 #hello]]
[[ a_markdown_filepath.md #hello]]
```

那么在 `a_markdown_filepath.md` 中，应该有个 Header 也指定了 hello 作为锚点的 key 作为对应，语法为当前行末尾增加 ` #key`。
```
this is a_markdown_filepath.md

##  Header 1
something here

## Header 2 #hello
the anchor of "hello" is in this header.
```

## 使用 Wiki 链接语法嵌入文档
如果文档的路径以 @ 结尾，那么在 Metion 的 Markdown 预览、渲染、导出的过程中，会自动把文档对应的内容，读取、解析并直接嵌入到当前文章中。这个功能仅限于 Wiki 的链接语法，不支持 Markdown 默认的链接语法。

下面的语法都是可以工作的：
```
[[ a_markdown_filepath@]]
[[ a_markdown_filepath.md@ | 我是实际显示的链接文本 #hello]]
[[ a_markdown_filepath.md@ #hello]]
```

## 点击与文档之间的跳转
键盘上按住 Alt 或者 Command 键，然后点击链接语法的内容，会跳转到对应的引用文档；如果对应的文档尚未创建，并且是使用 Wiki 风格的语法书写，则会自动进行新文档的创建。
如果需要跳转回原来的文档，建议使用 `Shift+Command+G` 这个快捷键，调出被引用的文档列表，再跳转回去。 

## Wiki 链接语法与 Tag
Metion 中，如果要使用 Tag ，需要在文章头部的 metadata 中进行声明，另外作为一个补充，就是可以使用 Wiki 链接语法来创建 Tag。 如果 `[[ ]]` 包裹的内部以 # 开头，则认为是 Tag（标签）的声明。
但需要注意的是，`[[ #MyTag ]]`  声明的标签是最终会被 Markdown 解析并作为文本显示的，不像 metadata 的声明是隐藏的。
```
Hello world, this is [[ #Tag ]] & [[ #Tag2 ]], it works.
```

## 注意事项
Wiki 链接语法构建的链接、Tag，以及普通 Markdown 的链接语法指向了某篇文档，Metion 可以构建彼此的关系链，但是它们最终由 Markdown 渲染之后的网页（包括预览界面）上，由于各方面的原因（比如技术性限制、上下文关联资源缺乏），实际的点击链接是无效的。

如果希望这部分关联性的链接在外部输出中也能承担更多的角色，则需要外部的渲染支持。比如 Wiki 链接语法风格，在 FarBox 2.0 某些 Wiki 的网站模板中能自动处理这些链接的跳转，另外 FarBox 2.0 也支持自行定义模板，以对应更复杂的页面渲染和关系。
