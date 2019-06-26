---
layout: post
title:  "遍历map和list"
categories: java
tags: java
author: 赵醒醒
---

* content
{:toc}

**遍历map**

1.这是最常见的并且在大多数情况下也是最可取的遍历方式。在键值都需要时使用。

```
Map<Integer, Integer> map = new HashMap<Integer, Integer>(); 
for (Map.Entry<Integer, Integer> entry : map.entrySet()) { 
  System.out.println("Key = " + entry.getKey() + ", Value = " + entry.getValue()); 
}
```
2.在for-each循环中遍历keys或values。

```
Map<Integer, Integer> map = new HashMap<Integer, Integer>(); 
//遍历map中的键 
for (Integer key : map.keySet()) { 
  System.out.println("Key = " + key); 
} 
//遍历map中的值 
for (Integer value : map.values()) { 
  System.out.println("Value = " + value); 
}
```
3.用迭代器迭代
```
Map<Integer, Integer> map = new HashMap<Integer, Integer>(); 
Iterator<Map.Entry<Integer, Integer>> entries = map.entrySet().iterator(); 
while (entries.hasNext()) { 
  Map.Entry<Integer, Integer> entry = entries.next(); 
  System.out.println("Key = " + entry.getKey() + ", Value = " + entry.getValue()); 
}
```
4.通过键找值遍历（效率低）

```
Map<Integer, Integer> map = new HashMap<Integer, Integer>(); 
for (Integer key : map.keySet()) { 
  Integer value = map.get(key); 
  System.out.println("Key = " + key + ", Value = " + value);
```

**遍历list**

1.超级for循环遍历

```
for(String attribute : list) {
  System.out.println(attribute);
}
```
2.对于ArrayList来说速度比较快, 用for循环, 以size为条件遍历

```
for(int i = 0 ; i < list.size() ; i++) {
  system.out.println(list.get(i));
}
```
3.用迭代器迭代

```
Iterator it = list.iterator();
while(it.hasNext()) {
  System.ou.println(it.next);
}
```
