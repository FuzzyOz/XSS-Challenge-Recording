# Level 11 (referer头截断)

观察一下f12发现和level10很相似，多了一个t_ref标签，尝试故技重施但是没有用。

尝试一下抓包，发现也没什么特别的，最终还是翻了师傅的wp，发现居然是加referer。。

在bp中加上<!--Referer:'' onmouseover=alert() type="text-->

# Level 12 (user-agent截断)

和上题思路相似，插入点在user-agent处

<!--User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:72.0) Gecko/20100101 Firefox/72.0 '' onmouseover=alert() type="text-->

# Level 13 (cookie截断)

相似，插入点在cookie处

<!--Cookie: '' onmouseover=alert() type="text-->

# Level 14

挂了。。。

# Level 15 (文件包含)

这题秀。菜鸡走不出来。提供佬的wp并尝试复现。

------

审计代码发现只有一个src变量是可以控制的

```html
<div ng-include="'myFile.htm'"></div>//此为AngularJS包含html文件
```

**ng-include** 指令用于包含外部的 HTML 文件。

包含的内容将作为指定元素的子节点。

ng-include属性的值可以是一个表达式，返回一个文件名。

默认情况下，包含的文件需要包含在同一个域名下。

包含level1内容

```
http://127.0.0.1/xss/level15.php?src='level1.php?name=<script>alert(1)</script>'
//这里的src加''是因为需要ng-include格式
//ng-incldue:'xxx.html'
//方能执行
```

发现并没有效果。。。

这里的ng-include 属于angular js，需要调用angular.min.js文件，不调用不能正常执行功能，测试下发现源码里用的是google的被墙了，所以改为新的

```
https://cdn.staticfile.org/angular.js/1.4.6/angular.min.js
```

------

到这里是佬的，我尝试了一下，如果不开科学上网，单纯改前端文件仍然调用墙外的google的js。

如果开科学上网，火狐是可以开启ng-include修改的但是我的火狐科学不了，chrome可以科学但是f12中ng-include选项被禁用了，所以我的复现失败，希望佬们一起来尝试看看。