---
layout: post
title:  "根据图片路径获取图片并转换位base64格式字符串"
categories: java
tags: java
author: 赵醒醒
---

* content
{:toc}

**使用的时候直接调用方法就行**
**根据图片路径获取图片并转换位base64格式字符串**
```
public static String ImageToBase64ByOnline(String imgURL) {
        ByteArrayOutputStream data = new ByteArrayOutputStream();
        try {
            // 创建URL
            URL url = new URL(imgURL);
            byte[] by = new byte[1024];
            // 创建链接
            HttpURLConnection conn = (HttpURLConnection) url.openConnection();
            conn.setRequestMethod("GET");
            conn.setConnectTimeout(5000);
            InputStream is = conn.getInputStream();
            // 将内容读取内存中
            int len = -1;
            while ((len = is.read(by)) != -1) {
                data.write(by, 0, len);
            }
            // 关闭流
            is.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
        // 对字节数组Base64编码
        BASE64Encoder encoder = new BASE64Encoder();
        return encoder.encode(data.toByteArray());
    }
```
**处理字符串再存入你们的服务器啥的**

```
String str = ImageToBase64ByOnline(url);
//记得把头给截取掉
str = str.substring(str.indexOf(',') + 1);
//base64字符串转换为比特数组
BASE64Decoder decoder =new BASE64Decoder();
byte[] imageByte = new byte[0];
 try {
     imageByte=decoder.decodeBuffer(str);
 }catch (IOException e) {
     e.printStackTrace();
     return;
 }
 //然后把imageByte传服务器
```
