The file "hosts" is the final list.

This hosts file that can help you visit Facebook, Twitter & Google (as well as YouTube).

If you want the list of any other sites, post domain names here, and I'll work out the new list.

列表可以访问哪些网站？
可以访问的网站包括FourSquare, DropBox, Google, Facebook以及Twitter。YouTube可以访问，但是不能看视频（主要是因为YouTube获取视频流的地址不支持https）。
另外，将这个Hosts列表导入到Android手机后，手机可以访问Twitter, Facebook的服务。对Facebook手机应用的支持还不是很好，我不知道Facebook的手机应用需要哪些Hosts，因此没有完整提供。

列表如何生成？
目前这个列表是在SSH服务器上通过脚本获取的。当然，脚本只是一种方式，个人认为，任何一个可以翻墙的代理都可以用来获取Hosts列表。
在这个列表生成以后，当中的很多IP实际上是不能访问的。这些IP将被放到我本地的数据库中进行检查。比如像之前Twitter的IP，在不断地发生变化，那么，在我本地的数据库中，就存有了Twitter的多个IP，从中选择一个可以访问的IP合并到最终的Hosts列表中去。

如何增加列表内容？
发现网站载入长时间没有完成时，可以在网页上点击右键，选择"审查元素"（Chrome）或者安装FireBug插件（Firefox），接着对于没有载入的页面获取它的域名。
比如，没有载入的页面是 https://github.com/davidsun/HostsFile ，那么，获取的域名就是 github.com 。
在获取了域名以后，可以直接在GitHub上提交这些域名，我会定期处理这些请求，并且扩充和更新列表。

脚本如何使用？
脚本是用Python编写的，执行方式为
    # python getHostsFile.py <输入文件名>
输入的格式见文件"hostsPool"，即，一行一个域名。


--------
By Davidsun (@sunzheng91)
http://pursuer.me
