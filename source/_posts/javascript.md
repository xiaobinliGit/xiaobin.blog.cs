---
title: JavaScript training--Session One
date: 2018-01-29 19:36:25
categories:
  - 技术日志
  - 语言
tags:
  -JavaScript
---
### 摘要: JavaScript Workshop
<!--more-->
去年下半年，在为期一年的项目忙完后，我们迎来的公司最大的重组，重组中很多组员进入到不同的领域，我们组也不例外，之前基于云做LTE Control Plan，重组后我们的大组的侧重点也转做Solution&Production，于是整个Squad Team从LTE CP直接转到CloudBTS OM（Operation and Management），语言也从之前熟悉的C/C++转为JavaScript，开始很好奇一个以通信为主的（虽然nokia现在正积极转型为软件为主）的公司，会使用互联网诞生的技术。但从最近一段时间的学习来看，也不是没有原因，JavaScript相比C++11，非常好上手，而且要管理庞大的通信平台，各种异步事件交互响应会非常频繁，但也要保证时效性，毕竟通信的时间粒度通常以毫秒为单位（LTE的TTI最小为1ms, WCDMA为2ms-80ms），而我们通过NodeJS提供的事件驱动框架（Promise），可以促成这一目的，当然，庞大的OM功能不可能这么简单，其中涉及到很多交互处理，当然不在这片文章的讨论范畴。毕竟刚开始上手，就从最近看的《JavaScript高级程序设计》开始，恰巧给team做了一个简单的training，顺带把材料放在这里，也算是一个时期的小小总结。
本次培训介绍了基本类型，函数，对象，原型，对原型这里只引入这个概念，更深层次的，比如寄生构造，稳妥构造等，会在下个Session继续介绍。

<div align=center>![1](/images/javascript/Slide1.BMP)</div>
<div align=center>![2](/images/javascript/Slide2.BMP)</div>
<div align=center>![3](/images/javascript/Slide3.BMP)</div>
<div align=center>![4](/images/javascript/Slide4.BMP)</div>
<div align=center>![5](/images/javascript/Slide5.BMP)</div>
<div align=center>![6](/images/javascript/Slide6.BMP)</div>
<div align=center>![7](/images/javascript/Slide7.BMP)</div>
<div align=center>![8](/images/javascript/Slide8.BMP)</div>
<div align=center>![9](/images/javascript/Slide9.BMP)</div>
<div align=center>![10](/images/javascript/Slide10.BMP)</div>
<div align=center>![11](/images/javascript/Slide11.BMP)</div>
<div align=center>![12](/images/javascript/Slide12.BMP)</div>
<div align=center>![13](/images/javascript/Slide13.BMP)</div>
<div align=center>![14](/images/javascript/Slide14.BMP)</div>
<div align=center>![15](/images/javascript/Slide15.BMP)</div>
<div align=center>![16](/images/javascript/Slide16.BMP)</div>
<div align=center>![17](/images/javascript/Slide17.BMP)</div>
<div align=center>![18](/images/javascript/Slide18.BMP)</div>
<div align=center>![19](/images/javascript/Slide19.BMP)</div>
<div align=center>![20](/images/javascript/Slide20.BMP)</div>
<div align=center>![21](/images/javascript/Slide21.BMP)</div>
<div align=center>![22](/images/javascript/Slide22.BMP)</div>
<div align=center>![23](/images/javascript/Slide23.BMP)</div>
<div align=center>![24](/images/javascript/Slide24.BMP)</div>
<div align=center>![25](/images/javascript/Slide25.BMP)</div>
<div align=center>![26](/images/javascript/Slide26.BMP)</div>
<div align=center>![27](/images/javascript/Slide27.BMP)</div>
<div align=center>![28](/images/javascript/Slide28.BMP)</div>
<div align=center>![29](/images/javascript/Slide29.BMP)</div>
<div align=center>![30](/images/javascript/Slide30.BMP)</div>
<div align=center>![31](/images/javascript/Slide31.BMP)</div>