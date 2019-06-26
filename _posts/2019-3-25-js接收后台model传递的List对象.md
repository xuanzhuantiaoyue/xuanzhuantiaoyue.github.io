---
layout: post
title:  "js接收后台model传递的List对象"
categories: javascript
tags: javascript
author: 赵醒醒
---

* content
{:toc}

**后台**
```
model.addAttribute("list", JSON.toJSONString(list));
```
**前台js**

```
var list= '${list}';
list = eval(list);
//然后打印出来的就是list了而不是对象
console.log(list);
```
**然后该干啥干啥**
