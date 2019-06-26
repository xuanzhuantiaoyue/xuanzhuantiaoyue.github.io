---
layout: post
title:  "js搜狐接口获取公网ip"
categories: javascript
tags: javascript
author: 赵醒醒
---

* content
{:toc}

```
<script src="http://pv.sohu.com/cityjson?ie=utf-8"></script>
<script type="text/javascript">
document.write(returnCitySN["cip"]+','+returnCitySN["cname"])
</script>
```
