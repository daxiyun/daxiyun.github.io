---
title:  Android 7、8、9 Captive Portal Server 地址修改 去除原生安卓WiFi图标的叉号
date:   2018-08-21 16:47:47 +0800
---

Android 默认情况下会经常访问这个地址 <a href="http://clients1.google.com/generate_204">http://clients1.google.com/generate_204</a> 用来探测网络状态。在每次连 Wi-Fi 时，也会访问一下这个地址。<br />但是访问 *.google.com 在国内是有问题的，所以我们需要修改这个设置。

<hr>

Android 7.x 、 8.x 、 9.x

<pre><code class="language-shell">adb shell &quot;settings put global captive_portal_http_url http://www.google.cn/generate_204&quot;;
adb shell &quot;settings put global captive_portal_https_url https://www.google.cn/generate_204&quot;;</code></pre>上面用的是 Google CN 的 /generate_204 地址，下面再列举几个其它常用的地址。

<pre><code class="language-shell">captive.v2ex.co
www.v2ex.com/generate_204
两个地址是等效的，由V2EX维护。
connect.rom.miui.com/generate_204
MIUI使用的地址，由小米公司维护。
www.qualcomm.cn/generate_204
国内很多ROM使用的地址，由高通中国维护。</code></pre>如果你的 Android 获取了 ROOT 管理员权限，可以安装 CaptiveMgr清除x和! 来快捷设置。<br /><a href="https://www.coolapk.com/apk/tech.evlsoc.captivemgr" title="CaptiveMgr清除x和! - 2.4 - 酷安网">CaptiveMgr清除x和! - 2.4 - 酷安网</a>

<!--210-->

