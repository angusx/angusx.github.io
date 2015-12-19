+++
date = "2015-12-18T21:36:34+08:00"
draft = true
title = "使用hugo和github pages写博客"

+++

#### 序
开始使用hugo githubpages写博客，这一次，要有点成绩了。

#### 搭建博客
1. 下载hugo [hugo release](https://github.com/spf13/hugo/releases),解压得到一个exe放到一个目录，将exe改为hugo.exe.然后在该目录打开 cmd，输入：
    ```
    >hugo new site gitpages
    ```
2. 此时得到一个gitpages目录。
```
▸ archetypes/
▸ content/
▸ layouts/
▸ static/
config.toml
```
   进入该目录，同时将hugo.exe复制到gitpages，创建一个about目录：
` >hugo new about.md` 会在content 目录生成一个about.md文件，可以添加简单的介绍。

3. 写博客，一般将博客文件放到content文件夹的post文件夹中：
	`>hugo new post\title.md` 会多出一个文件title.md。可以在里面添加内容。
4. 下载主题：[Hugo themes](http://themes.gohugo.io/)我选用的是[hugo slim主题](https://github.com/zhe/hugo-theme-slim)
5. 本地调试：
`>hugo server --theme=slim --buildDrafts --watch`
浏览器打开http://127.0.0.1:1313
就可以看到结果了。
6. 推送到github pages
```
git init
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:angusx/angusx.github.io.git
git push -u origin master
```
7. 文档 [hugo doc](https://gohugo.io/overview/introduction/)