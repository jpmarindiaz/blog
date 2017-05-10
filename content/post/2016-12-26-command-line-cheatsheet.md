---
title: Command line cheatsheet
lang: en
date: 2016-12-26T08:45:24-06:00
categories:
    - Dev
tags:
---


## Merge files into one

http://stackoverflow.com/questions/1653063/how-do-i-include-a-blank-line-between-files-im-concatenating-with-cat

```
ls -1 | while read f; do cat "$f"; done > ../../archive.json
```

