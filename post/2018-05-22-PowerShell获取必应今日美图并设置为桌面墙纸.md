---
title:  PowerShell获取必应今日美图并设置为桌面墙纸
date:   2018-05-22 17:36:41 +0800
---

<pre><code>#########################################################################
# PowerShell获取必应今日美图并设置为桌面墙纸
#########################################################################
function Save-BingTodayImage() {
#必应图片故事API
$bingImageApi =&#39;https://www.bing.com/HPImageArchive.aspx?format=xml&amp;idx=0&amp;n=1&amp;mkt=zh-cn&#39;
$bingUri = &#39;https://www.bing.com/&#39;
# 获取图片链接
Write-Host 正在下载，请稍后。
[xml]$bingImageXml = (Invoke-WebRequest -Uri $bingImageApi).Content
# Write-Host &quot; 今日图片故事： $( $bingImageXml.images.image.copyright ) &quot;
$imgLink = &#39;{0}{1}&#39; -f $bingUri , $bingImageXml.images.image.url
# 下载和保存图片
$imageDir = &quot;D:\OneDrive\BingWallpaper&quot;
if ( -not (Test-Path $imageDir) ) {
mkdir $imageDir | Out-Null
}
$imageFile = Join-Path $imageDir ( &#39;{0}.jpg&#39; -f $bingImageXml.images.image.enddate)
# 下载图片
Invoke-WebRequest -Uri $imgLink -OutFile $imageFile
return $imageFile
}
# 获取今日必应背景图片
$image=Save-BingTodayImage
Write-Host 下载已完成，正在设置壁纸。
#The code is from https://stackoverflow.com/questions/9440135/powershell-script-from-shortcut-to-change-desktop
Add-Type @&quot;
using System;
using System.Runtime.InteropServices;
using Microsoft.Win32;
namespace Wallpaper {
public enum Style : int {
Tile, Center, Stretch, NoChange
}
public class Setter {
public const int SetDesktopWallpaper = 20;
public const int UpdateIniFile = 0x01;
public const int SendWinIniChange = 0x02;
[DllImport(&quot;user32.dll&quot;, SetLastError = true, CharSet = CharSet.Auto)]
private static extern int SystemParametersInfo (int uAction, int uParam, string lpvParam, int fuWinIni);
public static void SetWallpaper ( string path, Wallpaper.Style style ) {
SystemParametersInfo( SetDesktopWallpaper, 0, path, UpdateIniFile | SendWinIniChange );
RegistryKey key = Registry.CurrentUser.OpenSubKey(&quot;Control Panel\\Desktop&quot;, true);
switch( style ) {
case Style.Stretch :
key.SetValue(@&quot;WallpaperStyle&quot;, &quot;2&quot;) ;
key.SetValue(@&quot;TileWallpaper&quot;, &quot;0&quot;) ;
break;
case Style.Center :
key.SetValue(@&quot;WallpaperStyle&quot;, &quot;1&quot;) ;
key.SetValue(@&quot;TileWallpaper&quot;, &quot;0&quot;) ;
break;
case Style.Tile :
key.SetValue(@&quot;WallpaperStyle&quot;, &quot;1&quot;) ;
key.SetValue(@&quot;TileWallpaper&quot;, &quot;1&quot;) ;
break;
case Style.NoChange :
break;
}
key.Close();
}
}
}
&quot;@
# 设置为桌面墙纸
[Wallpaper.Setter]::SetWallpaper( $image, 2 )
Write-Host 已完成，关闭并自动退出。
</code></pre><!--204-->

