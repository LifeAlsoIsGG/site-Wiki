---
layout: post
title: VS Code Pylint E1101 Module has no member 错误
slug: vs-code-pylint-e1101-module-has-no-member
date: 2020-01-09 09:28
status: publish
author: 熊猫小A
categories: 
  - 
tags: 
  - Python
  - VS Code
excerpt: 
---

VS Code 出现类似这样的问题：

```
Pylint E1101 Module 'torch' has no 'from_numpy' member...
```

这是 Pylint 的问题，三种方案都行：

## 行内禁用提示

```python
# pylint: disable=E1101
tensor = torch.from_numpy(np_array)
# pylint: enable=E1101
```

有点 ugly。

## 设置忽略提示

在 `.pylintrc` 中：

```
[MASTER]
extension-pkg-whitelist=numpy,torch,cv,cv2

[TYPECHECK]
ignored-modules=numpy,torch,cv,cv2
ignored-classes=numpy,torch,cv,cv2
```

也不是很优雅。

## 将 Member 指定为 generated

VS Code 设置：

```
"python.linting.pylintArgs": [
    "--errors-only",
    "--generated-members=numpy.* ,torch.* ,cv2.* , cv.*"
]
```

这个还可以。