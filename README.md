## 怎么使用chrome浏览器的timeline做页面性能分析
 * * *
Timeline面板记录和分析了web应用运行时的所有活动情况，这是研究和查找性能问题的最佳途径。

![](./img/timeline-panel.png)  

### TL;DR
*  在一个页面加载后或者用户操作结束，开始一个timeline记录来分析每个发生的事件  
*  在概述栏查看 FPS，CPU，network request  
*  点击一个柱状里面的事件查看详细的信息  
*  缩放记录的截面使分析更简单  


### Timeline panel overview
* * *
Timeline 栏由4个分栏组成  

1. **Controls**. 开始记录，停止记录， 在记录时捕获的参数信息  
2. **Overview**.   页面表现高水平的总结。详细信息如下文所示。
3. **Flame Chart**. CPU堆栈跟踪的可视化  

你可以看到一到三个点，许多垂直的竖线在你的火焰图上。蓝色的线表示DOMContentLocaded事件，绿色的线表示第一次绘制，红色的线表示加载的事件。

  1. **细节栏**， 当你选中一个事件时，这一栏会展示关于这个事件更多的信息。如果没有选中的事件，该栏会展示时间帧的信息。  
  
 ![](./img/timeline-annotated.png)  
  
 
#### Overview pane
**概述栏**由三个图表组成

   1. **FPS**. 每秒渲染的帧数，绿色的柱状条越高就表示每秒渲染的帧数越多。FPS图表中红色的块表明长帧，（表示页面渲染有性能问题的地方）  
   2. **CPU**. CPU资源， 这个区域的图表表明哪种事件占用CPU资源  
   3. **NET**. 每种颜色的条代表一个资源，条越长表示获取该资源的时间越长。颜色较轻的部分表示等待时间（从开始发出请求到第一个字节开始下载的时间）。颜色较深的部分表示数据传送时间（从第一个字节开始到最后一个字节下载完成的时间）。  
   
不同颜色的条表示如下  

*  HTML 文件是蓝色  
*  Script 文件是黄色  
*  Stylesheets 是紫色
*  Media 是绿色
*  Miscellaneour 资源是灰色

![](./img/overview-annotated.jpg)  

### Make a recording
***  
记录一个页面加载情况，打开浏览器的Timeline, 输入你想记录的页面，然后重新加载该页面。Timeline会自动记录重新加载的页面  

记录一个页面的交互情况，打开Timeline, 点击记录按钮 （ ● ）开始记录，或者使用键盘快捷方式 Cmd+E(Mac), Ctrl+E(Windows/Linux)。 正在记录时记录的按钮显示红色。 执行页面的交互，然后点击记录按钮或者使用键盘快捷方式停止记录  

当记录完成时，DevTools会猜测哪部分记录是你需要的，然后自动缩放到那一部分。


### Recording tips  
*  **让记录尽可能短**. 短时间的记录通常可以是分析更简单  

*  **避免无关的动作**. 避免像（鼠标点击，网络加载等等）和你所要记录和分析无关的动作。例如， 如果你想记录点击一个登陆按钮的情况，就不要滚动页面，加载图片等等

*  **关闭浏览器缓存**. 当你记录网络操作时，最好在DevTools Settings里面或者网络条件里面关闭 浏览器缓存

*  **关闭扩展**. chrome浏览器扩展会对你应用的Timeline记录增加不相关的影响。打开chrome浏览器隐身模式，或者创建一个新的chrome用户保证你的环境没有插件。


### View Recording details
***  
当你在火焰图里面选中一个事件时， **细节栏**里面会展示这个事件详细的信息  
![](./img/details-pane.png)
有一些tabs， 像 **Summary**,会展示所有的事件类型。其他tabs仅对某些事件类型可用。 查看每个记录类型的详细细节[Timeline event refrence](https://developers.google.com/web/tools/chrome-devtools/profile/evaluate-performance/performance-reference)   



### Capture screenshots during recording
***  
**Timeline**可以在页面加载的时候捕获截图。这个功能叫做幻灯片（**Filmstrip**） 
在你记录需要捕获页面截图之前需要在 **Controls**栏里面勾选 **Screenshots**复选框。 页面截图会显示在 **Overview**栏里面  

![](./img/timeline-filmstrip.png)
