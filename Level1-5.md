# Introduction

XSS攻击通常指的是通过利用网页开发时留下的漏洞，通过巧妙的方法注入恶意指令代码到网页，使用户加载并执行攻击者恶意制造的网页程序。这些恶意网页程序通常是JavaScript，但实际上也可以包括Java、 VBScript、ActiveX、 Flash  或者甚至是普通的HTML。攻击成功后，攻击者可能得到包括但不限于更高的权限（如执行一些操作）、私密网页内容、会话和cookie等各种内容。（摘自百度）

<!--<script>alert('xss')</script>-->

如上述的js语句就可以使网页弹窗显示xss，而正常的搜索语句不应该出现输入的js语句被执行的情况，所以这就是XSS漏洞。

（注：由于markdown直接粘代码会出现一些问题，故代码都放在注释中）

# Level 1

<!--<script>alert(1)</script>-->

# Level 2 (闭合输入框)

<!--"><script>alert(1)</script>-->

# Level 3 (htmlspecialchars)

htmlspecialchars会将特殊字符转义为html字符

& --> &amp

" --> &quot

' --> '

< --> &lt

(>) -->&gt (右箭头，markdown格式所以加了括号)

可以看到尖括号被转义了所以得用没有尖括号的特殊字符尝试。

<!--'onmouseover = 'javascript:alert(1)-->

onmouseover:鼠标指针移动到元素上触发。

可以看到单引号没有被转义，双引号被转义了所以只能用单引号。

# Level 4 (onmouseover)

和上一题差不多的payload: <!--"onmouseover="alert(1)-->

可f12看到源码最终为: <!--<input name="keyword" value="" onmouseover="alert(1)"-->

# Level 5 (超链接)

尝试"onmouseover=alert()，可以发现被加了下划线成了o_nmouseover

script也被加了，所以这两个方法无法使用。

但是<>未被转义，可以使用到Javascript超链接来触发，

payload: <!--" /><a href=javascript:alert("1");>x</a>"-->

点击出来的x链接就过了。

