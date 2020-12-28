---
title:  PHP读取图片并以ImageJpeg方式输出
date:   2015-05-14 13:03:02 +0800
---

classimgdata{<br />public$imgsrc;<br />public$imgdata;<br />public$imgform;<br />publicfunctiongetdir($source){<br />$this-&gt;imgsrc=$source;<br />}<br />publicfunctionimg2data(){<br />$this-&gt;_imgfrom($this-&gt;imgsrc);<br />return$this-&gt;imgdata=fread(fopen($this-&gt;imgsrc,&#39;rb&#39;),filesize($this-&gt;imgsrc));<br />}<br />publicfunctiondata2img(){<br />header(&quot;content-type:$this-&gt;imgform&quot;);<br />echo$this-&gt;imgdata;<br />//echo$this-&gt;imgform;<br />//imagecreatefromstring($this-&gt;imgdata);<br />}<br />publicfunction_imgfrom($imgsrc){<br />$info=getimagesize($imgsrc);<br />//var_dump($info);<br />return$this-&gt;imgform=$info[&#39;mime&#39;];<br />}<br />}<br />$n=newimgdata;<br />$n-&gt;getdir(&quot;$bing_jpg&quot;);<br />$n-&gt;img2data();<br />$n-&gt;data2img();<br />echo$n;&nbsp;

<!--144-->

