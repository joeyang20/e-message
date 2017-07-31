# 获取token失败

1.首先在服务器上执行：

```sh
ping api.cn.ronghub.com
```

看看是否能够通；

2.把`api.cn.ronghub.com`放到浏览器上运行，看是否能够出来页面，访问不到就是问题。

3.如果是linux环境上没有浏览器，可以试试：

```sh
wget api.cn.ronghub.com
curl api.cn.ronghub.com
```

看看是否能够获取到页面。
还有就是

```cmd
telnet api.cn.ronghub.com 80
telnet api.cn.ronghub.com 443
```

看是否能够正确响应。前两个命令是能够看到页面的源码。以上3个方法在没有浏览器的时候可以在linux主机上测试。

3.清理dns缓存，
windows上执行：

```cmd
ipconfig /flushdns
```

linux上：
如果是清除NSCD上的Cache，可重新启动NSCD服务来达成清除DNS Cache的效果。使用的命令：

```sh
service nscd restart
/etc/init.d/nscd restart
```

如果是清除BIND服务器上的CACHE，使用的命令是:

```sh
rndc flush
```

如果是用dnsmasq实现的DNS服务器，使用的命令是:

```sh
sudo /etc/init.d/dnsmasq restart
```