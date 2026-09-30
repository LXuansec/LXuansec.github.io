# LXuan 博客使用说明

这个网站使用 Hugo 和 PaperMod，文章使用 Markdown 编写。网站地址：https://lxuansec.github.io/。

## 1. 新建文章

推荐每篇文章使用一个独立文件夹，把正文和图片放在一起：

```bash
cd /home/elu/LXuanblog
hugo new content posts/my-first-post/index.md
```

`my-first-post` 是文章目录名，也会成为网址的一部分，建议使用小写英文和连字符。修改 `title` 不会改变这个目录名。

生成后的结构：

```text
content/posts/my-first-post/
├── index.md
├── example.png
└── diagram.jpg
```

`index.md` 是正文，图片按需复制到同一文件夹。

## 2. 编辑文章信息与正文

用任意文本编辑器打开 `index.md`。文件顶部两条 `---` 之间是文章信息，后面是正文：

````markdown
---
title: "我的第一篇博客"
date: 2026-09-30T16:00:00+08:00
draft: false
categories: ["杂谈"]
tags: ["学习笔记"]
summary: "这篇文章的简短介绍。"
---

## 第一节

这里写正文。支持 **加粗**、列表和 [链接](https://example.com)。

## 代码示例

```cpp
#include <iostream>

int main() {
    std::cout << "Hello, world!" << std::endl;
}
```

## 图片

![图片说明](example.png)
````

常用字段：

| 字段 | 用途 |
| --- | --- |
| `title` | 网页上显示的文章标题 |
| `date` | 文章日期，决定列表排序；未来日期的文章默认不会发布 |
| `draft` | `true` 是草稿，`false` 才会正式发布 |
| `categories` | 文章分类，决定首页进入哪个终端框 |
| `tags` | 具体知识点，可设置多个 |
| `summary` | 文章列表中的摘要；不写时由 Hugo 自动提取 |

## 3. 给文章分类

首页固定显示两个分类：**杂谈** 和 **CUDA and pytorch**。

杂谈文章填写：

```yaml
categories: ["杂谈"]
```

CUDA / PyTorch 文章填写：

```yaml
categories: ["CUDA and pytorch"]
tags: ["CUDA", "PyTorch", "GPU"]
```

推荐每篇文章设置一个主分类。需要多个分类时也可以填写：

```yaml
categories: ["杂谈", "CUDA and pytorch"]
```

这篇文章会同时出现在两个分类里。新分类随已发布文章自动显示；没有分类的文章归入“未分类”。固定的两个分类即使没有文章，也会保留空框。

每个首页分类终端显示最新 4 篇文章，可以通过底部入口进入分类页查看全部文章。

## 4. 添加图片

将图片放在文章目录中，使用相对路径引用：

```markdown
![运行结果](result.png)
```

也可以放进子目录：

```text
content/posts/my-first-post/
├── index.md
└── images/
    └── result.png
```

正文引用：

```markdown
![运行结果](images/result.png)
```

推荐图片文件名使用英文、数字和连字符，避免空格。不要填写本机绝对路径，例如 `/home/elu/Pictures/result.png`，否则上线后无法显示。

## 5. 本地预览

```bash
cd /home/elu/LXuanblog
hugo server -D
```

打开终端提示的地址，通常是 http://localhost:1313/。`-D` 会显示草稿，保存文件后页面会自动更新。按 `Ctrl+C` 停止服务；服务停止后，本地网址就无法访问。

如果要预览未来日期的文章：

```bash
hugo server -D --buildFuture
```

## 6. 提交并发布

确认文章的 `draft: false`，日期不是未来时间，然后执行：

```bash
cd /home/elu/LXuanblog
git status
git add content/posts/my-first-post/
git commit -m "Add my first post"
git push origin master
```

将 `my-first-post` 替换为实际文章目录。图片会随整个目录一起提交。

推送到 `master` 后，GitHub Actions 会自动使用 Hugo 构建并部署，不需要手工提交 `public/` 中的生成文件。

部署记录：https://github.com/LXuansec/LXuansec.github.io/actions

部署成功后访问 https://lxuansec.github.io/。如果仍显示旧页面，可按 `Ctrl+Shift+R` 强制刷新。

## 7. 修改已发布文章

编辑原来的 `index.md` 或图片，重复提交发布步骤即可。不要轻易改文章目录名，否则原来的文章链接会变化。

## 常见问题

- **文章没出现**：检查 `draft` 是否为 `false`、日期是否在未来，以及 GitHub Actions 是否部署成功。
- **图片不显示**：检查图片是否已提交，路径和文件名大小写是否一致。
- **本地预览拒绝连接**：重新运行 `hugo server -D`，并保持终端运行。
- **分类没有文章**：检查 `categories` 的名称是否与首页分类一致，不要把分类只写到 `tags` 中。
- **首页显示旧内容**：先检查部署状态，再强制刷新或使用无痕窗口。
