# Level 16 (绕空格)

利用keyword参数尝试，

第一次发现过滤了script和/ ，

第二次使用img标签发现空格被改成奇怪东西，

将空格改换编码，得到payload: <!--?keyword=<img%0asrc=1%0aonerror=alert(1)>-->

# Level 17 (编码过滤)

html实体代码过滤了尖括号和引号，所以可以使用on事件来实现弹窗。

payload :<!--?arg01=a&arg02=b onmouseover=alert(1)-->

奇怪的是我并没有过这一条，看了其他的wp也是这样过的，我再试试。。

# Level 18 

基本跟上一条一样的payload，同时我也没过。。

# Level 19-20 (flash xss)

需要对flash反编译分析源码，水平有限就贴个别人的wp大家看看。

## Level 19

flash xss，需要对flash的反编译对源码进行分析，这里使用jpexs-decompiler来分析，首先定位getURL函数

![img](https://upload-images.jianshu.io/upload_images/5808046-e28918d563bc6471.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

然后追踪到sIFR的内容

![img](https://upload-images.jianshu.io/upload_images/5808046-2dddef201790a5cd.png?imageMogr2/auto-orient/strip|imageView2/2/w/1132)

得知version参数可以传入loc4变量中，即sIFR的内容中，但是getURL只在内容为link时打开，所以分析contentIsLink函数

![img](https://upload-images.jianshu.io/upload_images/5808046-4bf632effb57afdd.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

所以我们可以构造<a > </a> 标签来传值

payload: <!--arg01=version&arg02=<a href="javascript:alert(1)">123</a>-->

再点击123即可弹窗

## Level 20

得下载这个东西zeroclipboard.swf，烧脑百度之后得知有漏洞利用的payload直接用了，嘻嘻。
可以参考这个大神发的文章http://www.freebuf.com/sectool/108568.html

payload：<!--arg01=id&arg02=\%22))}catch(e){}if(!self.a)self.a=!alert(/xss/)//%26width%26height-->

