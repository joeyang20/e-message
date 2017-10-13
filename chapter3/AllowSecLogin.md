# 设置允许账号二次登陆

## 解决：

1.客户端登陆不显示，白屏等错误，

![允许同一用户重复登录](/image/c3/后端设置允许同一用户重复登录.png "Title")

2.一种错误是repeatLanding错误，这类错误需要往数据库social_IMsessionkey表写入一条记录才可以：

```sql
把缺失的id补全：
insert into social_IMsessionkey(userid) values('');
```

3.升级了8月23号以后的包，导致因为兼容性设置而出现的，登陆页面没有出现，从而无法登陆的问题，需要设置程序的兼容性才能解决：

![设置兼容性](/image/c3/设置兼容性.png "Title")

4.打开控制台发现Not allowed to load local resource：（在客户端electron控制台上出现）

解析：现代浏览器由于安全考虑，像chrome具有的沙盒机制，没有办法直接访问本地静态资源，解决这个问题可以通过web服务器设置一个虚拟目录。然后设置这个目录的路径映射。