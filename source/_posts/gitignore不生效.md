---
title: gitignore不生效
date: 2018-04-07 11:22:28
tags: git
---

有时候会发现有这么一种情况，修改了.gitignore，但是文件却没有被屏蔽掉，非常蛋疼。
引发这个问题的原因是因为git里有缓存，于是三部曲第一步清缓存走起
```
git rm -r --cached .
git add .
git commit -m "update git ignore"
```

