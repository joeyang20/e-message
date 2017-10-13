# 设置允许账号二次登陆

为了解决客户端登陆不显示，白屏等错误，还有一种错误是repeatLanding错误，这类错误需要往数据库social_IMsessionkey表写入一条记录才可以：

```sql
把缺失的id补全：
insert into social_IMsessionkey(userid) values('');
```

![允许同一用户重复登录](/image/c3/后端设置允许同一用户重复登录.png "Title")

还有一个可能性就是：升级了8月23号以后的包，导致因为兼容性设置而出现的，登陆页面没有出现，从而无法登陆的问题，需要设置程序的兼容性才能解决：

![设置兼容性](/image/c3/设置兼容性.png "Title")