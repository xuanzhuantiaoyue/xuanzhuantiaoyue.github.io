---
layout: post
title:  "js中date转字符串"
categories: javascript
tags: javascript
author: 赵醒醒
---

* content
{:toc}

## Date转String

```
function formatDate(date) {
        var date = new Date(date);
        var y = date.getFullYear();
        var m = date.getMonth() + 1;
        var d = date.getDate();
        var hours = date.getHours();
        var minutes = date.getMinutes();
        var seconds = date.getSeconds();
        m = m > 9 ? m : '0' + m;
        hours = hours > 9 ? hours : '0' + hours ;
        minutes = minutes > 9 ? minutes : '0' + minutes ;
        seconds = seconds > 9 ? seconds : '0' + seconds ;
        return y + '-' + m + '-' + d + ' ' + hours + ':' + minutes + ':' + seconds;
    }
```
**必须加var date = new Date(date);**
否则会报 **UnCaught TypeError:date.getXXXXX is not a function**

## String转Date

```
var str= "2019-5-15 15:54:01";
str= str.replace(/-/g,"/");
var date = new Date(s );
```
/-/g 是正则表达式
表示将所有短横线-替换为斜杠/
其中g表示全局替换
