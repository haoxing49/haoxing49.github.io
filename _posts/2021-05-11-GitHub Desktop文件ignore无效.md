---
layout:     post
title:      GitHub Desktop文件ignore无效
subtitle:   GitHub Desktop文件ignore无效
date:       2021-05-11
author:     haoxing49
header-img: img/post-bg-debug.png
catalog: true
tags:
    - Git
    - GitHub
    - GitHub Desktop
---

- 原因:<br/>
因为gitignore只能忽略那些原来没有被`track`的文件，如果某些文件已经被纳入了版本管理中，则修改.gitignore是无效的
- 解决:<br/>
在命令窗口中输入如下命令:
```git
git rm -r --cached .
git add .
git commit -m "update .gitignore"
git push -u origin 自己的分支名称
```

---

来自文章【[.gitignore 无效解决方法](https://blog.csdn.net/wwwtotoro/article/details/91042307)】