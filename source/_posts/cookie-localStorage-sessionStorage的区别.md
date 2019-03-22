---
title: 'cookie, localStorage, sessionStorage的区别'
copyright: true
date: 2019-03-22 15:51:29
tags:
---

# cookie, localStorage, sessionStorage

[详说 Cookie, LocalStorage 与 SessionStorage](https://jerryzou.com/posts/cookie-and-web-storage/)

一、浏览器允许每个域名所包含的[cookie](https://www.baidu.com/s?wd=cookie&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)数：

[Microsoft](https://www.baidu.com/s?wd=Microsoft&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)指出 InternetExplorer8 增加[cookie](https://www.baidu.com/s?wd=cookie&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)限制为每个域名 50 个，但 IE7 似乎也允许每个域名 50 个[cookie](https://www.baidu.com/s?wd=cookie&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)。

Firefox 每个域名 cookie 限制为 50 个。

Opera 每个域名 cookie 限制为 30 个。

Safari/WebKit 貌似没有 cookie 限制。但是如果 cookie 很多，则会使 header 大小超过服务器的处理的限制，会导致错误发生。

注：“每个域名 cookie 限制为 20 个”将不再正确！

二、当很多的 cookie 被设置，浏览器如何去响应。

除 Safari（可以设置全部 cookie，不管数量多少），有两个方法：

最少最近使用（leastrecentlyused([LRU](https://www.baidu.com/s?wd=LRU&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao))）的方法：当 Cookie 已达到限额，自动踢除最老的 Cookie，以使给最新的 Cookie 一些空间。InternetExplorer 和 Opera 使用此方法。

Firefox 很独特：虽然最后的设置的 Cookie 始终保留，但似乎随机决定哪些 cookie 被保留。似乎没有任何计划（建议：在 Firefox 中不要超过 Cookie 限制）。

三、不同浏览器间 cookie 总大小也不同：

Firefox 和 Safari 允许 cookie 多达 4097 个字节，包括名（name）、值（value）和等号。

Opera 允许 cookie 多达 4096 个字节，包括：名（name）、值（value）和等号。

InternetExplorer 允许 cookie 多达 4095 个字节，包括：名（name）、值（value）和等号。

注：多字节字符计算为两个字节。在所有浏览器中，任何 cookie 大小超过限制都被忽略，且永远不会被设置。

另！！！
[WINDOWS](https://www.baidu.com/s?wd=WINDOWS&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)所有的文件都会有一个实际大小和储存大小。一般 Cookie 是文本文件，里面也就几行代码，应该只有几十字节(bytes),但是[WINDOWS](https://www.baidu.com/s?wd=WINDOWS&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)会在缓存盘里把这个文件定义到[KB](https://www.baidu.com/s?wd=KB&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)的级别了
