# 讨论组无法打开

## 现象说明：emessage的讨论组无法打开，点击报错如下图：

![打开讨论组报错](/image/点击设置按钮.PNG)

## 检查方法：

1.查询**mobileProperty**表，根据下面查询语句，如果查询有多条记录，就有问题，代表和融云访问的接口产生了多个udid，产生多套数据，

字段说明：

**rongAppUDIDNew** : 融云访问服务的udid,这个key应该只能有一个，系统内部与融云服务做交互用的，每一个key代表了一套数据，所以这个被修改会导致群组和联系人，甚至手机端消息同步出现问题

查询语句：

```sql
select * from mobileProperty where name = 'rongAppUDIDNew'
```

修改办法：需要把多余的记录删除，保证只有一条存在即可。
