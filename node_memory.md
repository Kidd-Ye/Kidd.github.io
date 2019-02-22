# webpack打包时提示内存溢出
>如图所示：
>
>![img](https://github.com/Kidd-Ye/Kidd.github.io/blob/master/img/p2.png)
>
>原因：
>
>CALL_AND_RETRY_LAST Allocation failed - JavaScript heap out of memory JavaScript堆内存不足。在 Node 中通过 JavaScript 使用内存时只能使用部分>内存，这就是我们编译项目时为什么会出现内存泄露了，因为前端项目如果非常的庞大，webpack 编译时就会占用很多的系统资源，如果超出了V8对 Node 默认的内存限制大小就会报错。
>

## 解决方法：
>安装插件，增加node服务器内存限制
>
>项目根目录执行以下代码
>
>```
>npm install -g increase-memory-limit
>```
>
>```
>increase-memory-limit
>```
>
>重新打包，问题得到解决。


