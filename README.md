


# Android 屏幕适配 #
## 术语和概念 ##
- **屏幕尺寸** <br/>
按屏幕对角测量的实际物理尺寸。单位是英寸，1英寸=2.54厘米。为简便起见，Android 将所有实际屏幕尺寸分组为四种通用尺寸：小、 正常、大和超大。
- **屏幕分辨率** <br/>
屏幕上物理像素的总数。单位是px，1px=1个像素点。一般以纵向像素*横向像素，如1920\*1080。添加对多种屏幕的支持时， 应用不会直接使用分辨率；而只应关注通用尺寸和密度组指定的屏幕 尺寸及密度。
- **屏幕密度** <br/>
每英寸上的像素点数，单位是dpi。屏幕像素密度与屏幕尺寸和屏幕分辨率有关。
Android 将所有屏幕密度分组为六种通用密度： 低、中、高、超高、超超高和超超超高。
密度无关像素 (dp|dip)：等于 160 dpi （480\*320）屏幕上的一个物理像素。1dp=1px。<br/>
><font color=#8B0000 >注：根据google官方文档说明，当前手机最接近为准。</font><br\>

----------
<table width=400 align="center" >
<tr><td align="center">名称</td><td align="center">像素密度</td></tr>
<tr><td>mdpi</td><td>160dpi</td></tr>
<tr><td>hdpi</td><td>240dpi</td></tr>
<tr><td>xhdpi</td><td>320dpi</td></tr>
<tr><td>xxhdpi</td><td>480dpi</td></tr>
<tr><td>xxxhdpi</td><td>640dpi</td></tr>
</table>
按照2：3：4：6：8的比例进行图片缩放

## 解决方案 ##
**方案一：支持各种屏幕尺寸**<br/>

- **使用wrap\_content、match\_parent、weight**<br/>
 计算公式如下：计算出的宽度=原来宽度+剩余空间所占百分比的宽度
![df](http://i.imgur.com/Y2wLUB1.png)
屏幕宽度 L<br/>
Button1 <br/>
 L +（L-2L）* 1/3 = L-1/3L= 2/3L   <br/>
Button2<br/>
 L + (L-2L) * 2/3 = L-2/3L= 1/3L   <br/>
![](http://i.imgur.com/0gG3anf.png)
Button1<br/>
 0 + L * 1/3 = 1/3L <br/>
Button2<br/>
 0 + L * 2/3 = 2/3L <br/>

- **使用相对布局，禁止绝对布局**；
- **使用限定符**<br/>尺寸限定符、最小宽度限定符、布局别名、屏幕方向限定符 
<table width=100%>
<tr><td>屏幕特性</td><td>限定符</td><td>说明</td></tr>
<tr><td rowspan=4>尺寸</td><td>small</td><td>适用于小尺寸屏幕的资源。 至少为 426dp x 320dp</td></tr>
<tr><td>normal</td><td>适用于正常尺寸屏幕的资源。（这是基线尺寸。）至少为 470dp x 320dp</td></tr>
<tr><td>large</td><td>适用于大尺寸屏幕的资源。至少为 640dp x 480dp</td></tr>
<tr><td>xlarge</td><td>适用于超大尺寸屏幕的资源。至少为 960dp x 720dp</td></tr>
<tr><td rowspan=8>密度</td><td>ldpi</td><td>适用于低密度 (ldpi) 屏幕 (~120dpi) 的资源。</td></tr>
<tr><td>mdpi</td><td>适用于中密度 (mdpi) 屏幕 (~160dpi) 的资源。（这是基线 密度。）</td></tr>
<tr><td>hdpi</td><td>适用于高密度 (hdpi) 屏幕 (~240dpi) 的资源。</td></tr>
<tr><td>xhdpi</td><td>适用于超高密度 (xhdpi) 屏幕 (~320dpi) 的资源。</td></tr>
<tr><td>xxhdpi</td><td>适用于超超高密度 (xxhdpi) 屏幕 (~480dpi) 的资源。</td></tr>
<tr><td>xxxhdpi</td><td>适用于超超超高密度 (xxxhdpi) 屏幕 (~640dpi) 的资源。此限定符仅适用于 启动器图标，请参阅上面的注。</td></tr>
<tr><td>nodpi</td><td>适用于所有密度的资源。这些是密度独立的资源。不管当前屏幕的密度如何，系统都不会 缩放以此限定符标记的资源。</td></tr>
<tr><td>tvdpi</td><td>适用于密度介于 mdpi 和 hdpi 之间屏幕（约为 213dpi）的资源。它并不是 “主要”密度组，主要用于电视，而大多数应用都不 需要它 — 对于大多数应用而言，提供 mdpi 和 hdpi 资源便已足够，系统将根据需要对其进行 缩放。如果发现必须提供 tvdpi 资源，应以 1.33*mdpi 的系数 调整其大小。例如，mdpi 屏幕的 100px x 100px 图像应该相当于 tvdpi 的 133px x 133px。</td></tr>
<tr><td rowspan=2>方向</td><td>land</td><td>适用于横屏（长宽比）的资源。</td></tr>
<tr><td>port</td><td>适用于竖屏（高宽比）的资源。</td></tr>
<tr><td  rowspan=2>纵横比</td><td>long</td><td>适用于纵横比明显高于或宽于（分别在竖屏 或横屏时）基线屏幕配置的屏幕的资源。</td></tr>
<tr><td>notlong</td><td>适用于使用纵横比类似于基线屏幕 配置的屏幕的资源。</td></tr>
</table>

例：<br/>
res/layout/my\_layout.xml &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;//默认情况 (单面板)<br/>
res/layout-large/my\_layout.xml&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;//大屏幕情况（双面板）<br/>
res/layout-xlarge/my\_layout.xml &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;//超大屏幕<br/>
res/layout-xlarge-land/my\_layout.xml &nbsp;//超大屏幕横屏<br/>

> 屏幕尺寸的新配置限定符（在 Android 3.2 中引入）：<br/>
最小宽度限定符  res/layout-sw600dp/my_layout.xml   //双面板

为了减少对不同尺寸带来的布局维护困难问题，因此使用布局别名；<br/>

| 种类布局路径 |  描述 | 
| :----  | :-----  |
| res/layout/main.xml   | 单面板布局   |
| res/layout/main_twopances.xml    |  双面板布局   |

| 布局别名路径 |  描述 | 
| :----  | :-----  |
| res/values/layouts.xml          | 默认布局   显示单面板               |
| res/values-xlarge/layouts.xml   | android3.2之前的平板布局 显示双面板  |
| res/val ues-sw600dp/layouts.xml | android3.2之后的平板布局 显示双面板  |

布局别名文件内容：<br/>
> res/values/layouts.xml <br/>
&nbsp;&nbsp;<resources\><br/>
    &nbsp;&nbsp; &nbsp;< item name="main" type="layout">@layout/main</ item><br/>
&nbsp;&nbsp;</resources\> <br/> 

> res/values-xlarge/layouts.xml    
&nbsp;&nbsp;<resources\><br/>
&nbsp;&nbsp;&nbsp;&nbsp;< item name="main" type="layout">@layout/main_twopances</ item><br/>
&nbsp;&nbsp;</resources\> <br/>   

> res/val ues-sw600dp/layouts.xml <br/>
&nbsp;&nbsp; <resources\><br/>
  &nbsp;&nbsp; &nbsp;&nbsp; < item name="main" type="layout">@layout/main_twopances</ item><br/>
&nbsp;&nbsp; </resources\><br/>

> 注：在setContentView(R.layout.main);在此resID需要使用布局别名；

<p><br/>
不同密度下存放的图片  (按照2：3：4：6：8的比例)<br/>
res/drawable-mdpi/graphic.png  &nbsp;&nbsp; &nbsp;&nbsp; 48\*48<br/> 
res/drawable-hdpi/graphic.png  &nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;72\*72<br/>
res/drawable-xhdpi/graphic.png &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;96\*96<br/>
res/drawable-xxhdpi/graphic.png  &nbsp;&nbsp;&nbsp; 148\*148<br/>
res/drawable-xxxhdpi/graphic.png  &nbsp;&nbsp; 198\*198<br/>

屏幕方向限定符<br/>
res/values-sw600dp-land/layout.xml<br/>
res/values-sw600dp-port/layout.xml<br/>

- **使用自动拉伸位图（点9图）**

----------
## 总结 ##
|    android屏幕情况  |    layout |
|  :---------------  |  :------- |
|小屏幕，纵向       |单面板|
|小屏幕，横向       |单面板|
|7寸平板电脑，纵向   |单面板，带操作栏|
|7寸平板电脑，横向   |双面板，宽，带操作栏|
|10寸平板电脑，纵向  |双面板，窄，带操作栏|
|10寸平板电脑，横向  |双面板，宽，带操作栏|
|电脑，横向         |双面板，宽，带操作栏|
   
 
根据以上情况需要创建4种布局、使用布局别名绑定布局，如下所示:
 
|  |  |
| :----------- | :------------ |
res/layout/onepane.xml          |  //单面板
res/layout/onepane_with_bar.xml |  //单面板带操作栏
res/layout/twopane.xml          |  //双面板，宽布局
res/layout/twopane_narrow.xml   |  //双面板，窄布局
|||
res/values/layout.xml              | //@layout/onepane 
res/values-sw600dp-land/layout.xml | //@layout/twopane
res/values-sw600dp-port/layout.xml | //@layout/onepane_with_bar
res/values-xlarge-land/layout.xml  | //@layout/twopane 
res/values-xlarge-port/layout.xml  | //@layout/twopane_narrow


--------------------------------------
# 
**方案二：支持各种屏幕密度**<br/>
使用非密度制约像素(解决屏幕宽度不一致问题)
MakeXml.class 批量生成values-480\*320等文件下的lay\_x.xml及lay\_y.xml
![](http://i.imgur.com/f3kvHZ9.png)
提供备用位图 <br/>
所提供的图片不能乱放，应放于该像素的文件中，android会按照一定的比例在手机上显示，例如将
一张高分辨的图片放到低分辨率的文件夹中，在高分辨率的手机上显示这张图片会在原来的基础上放大。<br/>
#
**方案三：实施自适应用户界面流程** <br/>
可参照官方demo   NewsReader  
