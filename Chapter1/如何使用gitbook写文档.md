# 第1节:如何使用gitbook写文档
content is refer from :https://blog.csdn.net/lu_embedded/article/details/81100704
# what is GitBook?

GitBook is commond line tool which is base on Node.js ,it supports  both Markdown and AsciiDoc grammar format ，and can output ebook in form of HTML、PDF、eBook .etc。
---

so you can define  GitBook as a profile transfer tool.
---


所以，GitBook 不是 Markdown 编辑工具，也不是 Git 版本管理工具。市面上我们可以找到很多 Markdown 编辑器，比如 Typora、MacDown、Bear、MarkdownPad、MarkdownX、JetBrains’s IDE（需要安装插件）、Atom、简书、CSDN 以及 GitBook 自家的 GitBook Editor 等等。

因为gitbook editor 需要翻墙注册，所以推荐了 GitBook + Typora + Git

# how to install?

 GitBook + Typora + Git


- Node.js 下载地址：<https://nodejs.org/en/download/>
 因为 GitBook 是基于 Node.js，所以我们首先需要安装 Node.js
 现在安装 Node.js 都会默认安装 npm（node 包管理工具），所以我们不用单独安装 npm，打开命令行，执行以下命令安装 GitBook：
```
npm install -g gitbook-cli
```
- Typora 下载地址：<https://typora.io/> 　Typora 的安装很简单，难点在于需要翻墙才能下载
- Git 下载地址：<https://git-scm.com/downloads>

# how to use 

1.首先找到一个文件夹,并输入:

```powershell
:temp admin$ mkdir mybook
:temp admin$ cd mybook
:mybook admin$ gitbook init
warn: no summary file in this book
info: create README.md
info: create SUMMARY.md
info: initialization is finished
:mybook admin$ ls
README.md	SUMMARY.md
```

2.然后就会看到，多了两个文件:

- README.md —— 书籍的介绍写在这个文件里
- SUMMARY.md —— 书籍的目录结构在这里配置

3.使用Typora将文件夹打开：

![image-20190410150225259](/Users/qz.zzm/Library/Application Support/typora-user-images/image-20190410150225259.png)

编辑 SUMMARY.md 文件，内容修改为：
```markdown
# Summary

* [Introduction](README.md)
* [chapter 1](Chapter1/README.md)
  * [first page：a](Chapter1/a.md)
  * [second page：b](Chapter1/b.md)
* [chapter 2](Chapter2/README.md)
```

然后回到文件夹, 执行,可以看到自动创建了相关的文件和文件夹

```shell
:mybook admin$ gitbook init
info: create Chapter1/README.md
info: create Chapter1/a.md
info: create Chapter1/b.md
info: create Chapter2/README.md
info: create SUMMARY.md
info: initialization is finished
:mybook admin$ ls
Chapter1	Chapter2	README.md	SUMMARY.md
:mybook admin$ cd Chapter1
:Chapter1 admin$ ls
README.md	a.md		b.md
:Chapter1 admin$ cd ..
:mybook admin$ cd Chapter2
:Chapter2 admin$ ls
README.md
:Chapter2 admin$ cd ..
:mybook admin$ gitbook serve
Live reload server started on port: 35729
Press CTRL+C to quit ...

info: 7 plugins are installed
info: loading plugin "livereload"... OK
info: loading plugin "highlight"... OK
info: loading plugin "search"... OK
info: loading plugin "lunr"... OK
info: loading plugin "sharing"... OK
info: loading plugin "fontsettings"... OK
info: loading plugin "theme-default"... OK
info: found 5 pages
info: found 0 asset files
info: >> generation finished with success in 0.6s !

Starting server ...
Serving book on http://localhost:4000
```

接着我们执行 `gitbook serve` 来预览这本书籍，执行命令后会对 Markdown 格式的文档进行转换，默认转换为 html 格式，最后提示 “Serving book on [http://localhost:4000](http://localhost:4000/)”

![image-20190410153937568](/Users/qz.zzm/Library/Application Support/typora-user-images/image-20190410153937568.png)



当你写得差不多，你可以执行 gitbook build 命令构建书籍，默认将生成的静态网站输出到 _book 目录。实际上，这一步也包含在 gitbook serve 里面，因为它们是 HTML，所以 GitBook 通过 Node.js 给你提供服务了。 
build 命令可以指定路径：
```$ gitbook build [书籍路径] [输出路径]```
serve 命令也可以指定端口：
```$ gitbook serve --port 2333```　　
生成 PDF 格式的电子书：
```$ gitbook pdf ./ ./mybook.pdf```
生成 epub 格式的电子书：
```$ gitbook epub ./ ./mybook.epub```
生成 mobi 格式的电子书：
```$ gitbook mobi ./ ./mybook.mobi```