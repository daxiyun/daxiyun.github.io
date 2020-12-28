---
title:  简单实现 仿 JQuery 的 Ajax 的使用方法
date:   2017-08-05 16:26:13 +0800
---

默认为 POST ，如需 GET 需要传递参数。<br />JSyb.ajax({<br />type:&quot;GET&quot;,<br />url:&quot;pin.php&quot;,<br />callback:function(data){<br />JSyb.id(&#39;info&#39;).innerHTML=data;<br />}<br />});

JSyb.ajax({<br />url:&quot;i.php&quot;,<br />data:{&quot;pin&quot;:JSyb.id(&quot;pin&quot;).value},<br />callback:function(data){<br />JSyb.id(&#39;info&#39;).innerHTML=data;<br />}<br />});&nbsp;

<!--169-->

