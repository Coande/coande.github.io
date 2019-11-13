---
title: 畅言、多说评论转移到Valine
date: 2019-10-04 01:20:25
tags:
---

国庆假期，有时间就折腾一下，将畅言换掉，记录一下。

### 吐槽一下

> 自从多说关闭后，畅言支持导入多说评论，顺手就换了畅言。界面丑了点，但是没广告，还好。不知道从什么时候开始，出了个商业版，同时，免费版的评论列表加入了广告，页面还加入了浮动广告，有点恶心了~
>
> 作为一个评论管理后台，一个方便查看所有评论的入口都没有，需要填入适当条件进行搜索才能看到评论。
>
> 更要命的是不支持全部导出，只能导出最近一个月内的评论。
>
> 还有很多BUG和影响体验的操作，不知道是不是故意所为。可能是干不下去了，逼着用户离开？

<!-- more -->

### 导出畅言数据

写了个游猴脚本：

```
// ==UserScript==
// @name         畅言（云评论）导出脚本
// @namespace    https://e12e.com/
// @version      0.1
// @description  畅言（云评论）导出脚本（仅导出当前页文章列表的所有评论）
// @author       Coande
// @match        http://changyan.kuaizhan.com/audit/topics/AUDITED/TIME_DESC/*
// @grant        GM_xmlhttpRequest
// ==/UserScript==

(function() {
    'use strict';

    // 设置 appid，按需更改
    const CLIENT_ID = "cytls1bCh";

    const rows = $("body > div.container-self > div.content > div > div > table.table.table-hover.table-striped > tbody > tr");
    // 删除多余的表头行
    rows.splice(0, 1);

    // 收集文章相关信息
    const topicArr = [];
    rows.each((index, row) => {
        const topicId = $(row).find("a").eq(1).attr("href").split("/")[3];
        const topicTitle = $(row).find("a").eq(0).text();
        const topicUrl = $(row).find("a").eq(0).attr("href");
        topicArr.push({
            topicId,
            topicTitle,
            topicUrl
        });
    });
    // 根据 topicId 获取评论列表的API
    const url = "http://changyan.sohu.com/api/2/topic/comments?client_id=CLIENT_ID&page_size=10000&topic_id=TOPIC_ID&page_no=1&_=1570031307391";

    // 循环获取本页主题所有评论
    const commentArr = [];
    topicArr.forEach((topic, index) => {
        const targetUrl = url.replace("CLIENT_ID", CLIENT_ID).replace("TOPIC_ID", topic.topicId);

        GM_xmlhttpRequest({
            method: "GET",
            url: targetUrl,
            onload: function(response) {
                //这里写处理函数
                const jsonResult = JSON.parse(response.responseText);
                jsonResult.topic_title = topic.topicTitle;
                jsonResult.topic_url = topic.topicUrl;
                commentArr.push(jsonResult);

                // 全部数据获取完毕
                if (commentArr.length == topicArr.length) {
                    const blob = new Blob([JSON.stringify(commentArr, null, 2)], {
                        type: "text/plain;charset=utf-8"
                    });
                    const objUrl = URL.createObjectURL(blob);
                    const buttonObjString = '<a style="margin-right : 30px; float: right;" id="save-forum-setting"><button class="cy-btn" >导出本页文章所有评论</button></a>';
                    const buttonObj = $(buttonObjString).attr("href", objUrl).attr("download", "changyan-raw.json");

                    // 显示导出按钮
                    $("body > div.container-self > div.content > div > div > table:nth-child(1) > tbody > tr > td:nth-child(2)").append(buttonObj);
                }
            }
        });
    });
})();
```

脚本生效页面：

http://changyan.kuaizhan.com/audit/topics/AUDITED/TIME_DESC/1



### 畅言数据转为 Valine 数据

https://github.com/Coande/changyan-to-valine

### 多说数据转为 Valine 数据

不知道什么原因，之前多说的数据导入畅言后，感觉很多评论用户的名称丢失了。还有就是，畅言中的数据明显比多说的数据少，可能是被审查删掉了？所以，还是原多说导出的数据更靠谱。

https://github.com/Coande/duoshuo-to-valine

### 加入 Valine 的支持

参看：https://valine.js.org/quickstart.html

部分主题修改方法：https://valine.js.org/hexo.html

我用的是 hexo-theme-yilia 主题，所以参照这个改：

https://github.com/litten/hexo-theme-yilia/pull/646

改完后重新生成一下主题。

安装依赖是可能 `node-sass` 会报 404，原来`3.9.3`版本已经不存在了，改为`4.9.1`就好了。

重新生成主题后，记得删掉`node-modules`目录，否则可能导致以下错误：

```
Ineffective mark-compacts near heap limit Allocation failed - JavaScript heap out of memory
```