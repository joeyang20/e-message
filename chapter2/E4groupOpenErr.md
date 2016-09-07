# 讨论组无法打开

### 现象说明：emessage的讨论组无法打开，点击报错如下图：

![打开讨论组报错](/image/点击设置按钮.PNG)

#### 检查方法：

* 1.查询**mobileProperty**表，根据下面查询语句，如果查询有多条记录，就有问题，代表和融云访问的接口产生了多个udid，产生多套数据，

查询语句：`select * from mobileProperty where name = 'rongAppUDIDNew'`;

修改办法：需要把多余的记录删除，保证只有一条存在即可。
