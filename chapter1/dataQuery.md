# 数据库相关查询

### 历史记录

* 客户端历史记录是存放在数据库表`historymsg`之中，目前暂时没有单独管理消息的界面，如果需要删除某些聊天记录，需要到数据中执行相关删除语句，下面语句作为参考：
```
delete from historymsg where fromuserid = '84'
and targetid = '58717c95-76da-430f-8548-00b351815346'
and msgid in ('d2a7d02b-37d1-4b50-b93f-1e919ad22477','48bce6ee-8912-4064-98a6-f7a8bc22a54b','0e10fcd2-ba05-4844-8bcd-e13e0457ae4c') 
```
* fromuserid：代表发送的人，targetid：代表接收的对象，可以某个人的id（单聊），也可以是群组id（群聊），msgid：指的是消息id，单指某条消息

### 上传附件
* 用下面的语句可以查询在客户端上传的所有附件的信息：
```
select b.imagefilename as 文件名,b.filerealpath as 文件路径,b.imagefiletype as 文件类型 from ImageFile b
where exists(select 1 from social_IMFile where fileid = b.imagefileid)
```