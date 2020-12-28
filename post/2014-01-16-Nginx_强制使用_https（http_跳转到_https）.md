---
title:  Nginx 强制使用 https（http 跳转到 https）
date:   2014-01-16 14:36:11 +0800
---

强制使用 https（http 跳转到 https），最常见的是配置两个主机，一个监听 80，一个监听 443，监听 80 的那个直接转发到 443。

再不常见的方法还有：合并 http/https 主机，检测 $server_port = 80、$scheme = http 或发送 error code 497 等。

$server_port 是浏览器请求到达的服务器端口号；$scheme 是所用的协议，有 http 和 https，不过使用 $ssl_protocol 和这两种检测方法对于 http://www.sinosky.org:443 无效，最典型的例子就是 phpMyAdmin 在登录时会请求 http://www.sinosky.org:443。

497 是 nginx 的状态码，意思是 The plain HTTP request was sent to HTTPS port，虽然也能起到跳转的作用，但返回到客户端是 302 而不是 301，不过对于 http://www.sinosky.org:443 有效，建议配合前面 3 种方法一块使用。

下面是 3 种方法的示例

if($server_port=80){<br />return301https://$server_name$request_uri;<br />}<br />if($scheme=http){<br />return301https://$server_name$request_uri;<br />}<br />error_page497https://$server_name$request_uri;

来自：<a class="md_compiled" href="https://yusky.me/lnmp-enable-ssl-spdy.html">LNMP 全站部署 SSL &amp; SPDY</a>

<!--95-->

