---
layout:     post
title:      Git文件ignore无效
subtitle:   Git文件ignore无效
date:       2021-05-11
author:     haoxing49
header-img: img/post-bg-debug.png
catalog: true
tags:
    - Git
---
- 原因:<br/>
因为gitignore只能忽略那些原来没有被`track`的文件，如果某些文件已经被纳入了版本管理中，则修改.gitignore是无效的
- 解决:<br/>
```git
git rm -r --cached .
git add .
git commit -m "update .gitignore"
git push -u origin master
```
---
参考文章【[.gitignore 无效解决方法](https://blog.csdn.net/wwwtotoro/article/details/91042307)】