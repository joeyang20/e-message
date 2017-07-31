# 数据库相关查询

## 历史记录

客户端历史记录是存放在数据库表`historymsg`之中，目前暂时**没有单独管理消息**的界面，如果需要删除某些聊天记录，需要到数据中执行相关删除语句，下面语句作为参考，需要注意**删除后，客户端将不能展示被删除的聊天记录**：

```sql
delete from historymsg where fromuserid = '84'
and targetid = '58717c95-76da-430f-8548-00b351815346'
and msgid in ('d2a7d02b-37d1-4b50-b93f-1e919ad22477','48bce6ee-8912-4064-98a6-f7a8bc22a54b','0e10fcd2-ba05-4844-8bcd-e13e0457ae4c');
```

fromuserid：代表发送的人，targetid：代表接收的对象，可以某个人的id（单聊），也可以是群组id（群聊），msgid：指的是消息id，单指某条消息

## 上传附件

用下面的语句可以查询在客户端上传的所有附件的信息：

```sql
select b.imagefilename as 文件名,b.filerealpath as 文件路径,b.imagefiletype as 文件类型 from ImageFile b
where exists(select 1 from social_IMFile where fileid = b.imagefileid);
```

## 群组操作

根据群组名称可以删除群关系：

```sql
delete from mobile_ronggroup where group_id in (select targetid from social_IMConversation a where a.targetname in ('公司发文','文书科交流群','马钢协同办公系统'))
delete  from social_ImGroup_Rel where groupname in ('公司发文','文书科交流群','马钢协同办公系统');
```

## 名片相关的表

```sql
select * from SOCIAL_IMCHATRESOURCESHARE;
```

## 组织架构查询

查询总部下分所有下级分部（supsubcomid=0）

```sql
select id,subcompanyname from HrmSubCompany where supsubcomid=0 and (canceled is null or canceled<>1) order by showorder asc , subcompanyname asc;
```

查询总部下分部的部门列表（subcompanyid1=0）

```sql
select id,departmentname from HrmDepartment where subcompanyid1=0 and (canceled is null or canceled<>1) and supdepid=0 order by showorder asc, departmentname asc;
```

查询部门下直接人员

```sql
select id,lastname,loginid,messagerurl from HrmResource where departmentid='部门id' and status in(0,1,2,3) order by dsporder;
```