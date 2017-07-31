# 查询融云数据需要提供的数据

融云查消息需要的条件：
提供你们的appKey，userId，延迟的消息内容，大概时间，哪种消息类型（单聊还是群聊或者讨论组）
--获取发送者id和接受者id

```sql
select id from hrmresource a where a.loginid = '登录名';
```

--获取appkey,可以根据客户类型在后台查到    ---mgb7ka1nbxz9g
--确定消息类型和消息内容还有发送时间   --单聊
群聊 查群主id
//泛微定义的udiid

```sql
select propValue from mobileProperty a where a.name = 'rongAppUDIDNew';
```

删掉该值，测试和正式就不会乱了

```sql
delete from mobileProperty  where name = 'rongAppUDIDNew';
```

图片   RC:ImgMsg
附件   FW:attachmentMsg
样式：

```txt
12月5号-12月7号左右，appkey= z3v5yqkbvzwr0 ,userid=98,在群聊组id=ce3abaa1-8572-4621-b9c6-6a142f2ef094 ，的群组里面发送了好几个文件，但是消息记录没有把这些文件加载出来，这些记录相当于丢失了，能不能帮我查一下为什么没有记录吗，服务端有没有保存到这些消息记录？
12月21日，早上9点多，appkey = mgb7ka1nbxz9g ，id = 1071 
```

单聊：

```sql
select id from hrmresource a where a.loginid ='发送者登录名'；
select id from hrmresource a where a.loginid ='接收者登录名'；
select propValue from mobileProperty a where a.name = 'rongAppUDIDNew';
```

群聊：
需要提供群id