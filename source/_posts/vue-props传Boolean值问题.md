---
title: vue props传Boolean值问题
date: 2019-01-22 17:34:43
tags:
---

一直以为父组件为子组件传递`true`（Boolean值）可以这样传：
```
<component disabled />
```
今天偶然发现需要满足一定的条件才行。

<!-- more -->
这个和子组件的pros验证有关系，以下方式获取到都是一个空字符串（相当于false）

```
props: {
  disabled: {
    type: [Boolean, String],
    default: false
  }
}

props: {
  disabled: {
    default: false
  }
}

```

需要设置验证类型仅为Boolean时才能得到`true`（Boolean值）：

```
props: {
  disabled: {
    type: [Boolean],
    default: false
  }
}
```