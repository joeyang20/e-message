# 数据库相关查询

## 历史记录

客户端历史记录是存放在数据库表`historymsg`之中，目前暂时**没有单独管理消息**的界面，如果需要删除某些聊天记录，需要到数据中执行相关删除语句，下面语句作为参考，需要注意**删除后，客户端将不能展示被删除的聊天记录**：

```sql
delete from historymsg where fromuserid = '84'
and targetid = '58717c95-76da-430f-8548-00b351815346'
and msgid in ('d2a7d02b-37d1-4b50-b93f-1e919ad22477','48bce6ee-8912-4064-98a6-f7a8bc22a54b','0e10fcd2-ba05-4844-8bcd-e13e0457ae4c');
```

fromuserid：代表发送的人，targetid：代表接收的对象，可以某个人的id（单聊），也可以是群组id（群聊），msgid：指的是消息id，单指某条消息

消息记录后台查询的表，私有云聊天记录返回查询语句

```sql
select *
  from (select A.*, rownum rn
          from (select id,
                       fromUserId,
                       targetId,
                       targetType,
                       GroupId,
                       classname,
                       msgContent,
                       extra,
                       type,
                       imageUri,
                       dateTime,
                       msgid,
                       fullAmount
                  from HistoryMsgRecently
                 where groupid =
                   and dateTime < to_char('2061-10-1','yyyy-mm-dd')
                   and classname not in
                       ('FW:CountMsg',
                        'FW:SyncQuitGroup',
                        'FW:SyncMsg',
                        'FW:SysMsg',
                        'FW:ClearUnreadCount') order  by dateTime desc) A
         where rownum <= 10)
 where rn >= 1
 order by dateTime desc;
```

## 附件操作

用下面的语句可以查询在客户端上传的所有附件的信息：

```sql
select b.imagefilename as 文件名,b.filerealpath as 文件路径,b.imagefiletype as 文件类型 from ImageFile b
where exists(select 1 from social_IMFile where fileid = b.imagefileid);
```

删除发错的附件：

1.先从数据库里面查出来，发送的文件的物理位置：

```sql
select imagefileid, imagefilename, filerealpath from ImageFile where imagefileid in (select fileid from social_IMFile b ,hrmresource a where b.userid = a.id and a.loginid = '发送人登录名')
and imagefilename like '%文件名%'
and imagefileid in (select fileid from social_IMFile b ,hrmresource a where b.targetid = a.id and a.loginid = '接收文件人登录名');
```

2.根据查询的记录到oa服务器上找到对应的物理文件，删除掉，这样就不会被下载下来了，

3.最后删除文件列表里面的记录：

```sql
delete from social_IMFile a where a.fileid = '上一步求出来的文件id'
delete from social_IMFileShare a where a.fileid  = '上一步求出来的文件id'
```

## 群组操作

根据群组名称可以删除群关系：

```sql
delete from mobile_ronggroup where group_id in (select targetid from social_IMConversation a where a.targetname in ('公司发文','文书科交流群','马钢协同办公系统'))
delete  from social_ImGroup_Rel where groupname in ('公司发文','文书科交流群','马钢协同办公系统');
```

删除重复的群聊分组关系：

```sql
delete from social_ImGroup_Rel where id  not in (select min(id) from social_ImGroup_Rel group by groupId,userId having count(id)>1)
and id not in (select min(id) from social_ImGroup_Rel group by groupId,userId having count(id)=1)
```

查询重复的群聊分组关系：

```sql
select groupId,userId from social_ImGroup_Rel group by groupId,userId having count(id)>1
```

初始化群聊分组关系：

```sql
delete from social_ImGroup_Rel;

insert into social_ImGroup_rel (rel_id,userid,groupid,groupName,isopenfire)
select (select id from social_ImGroup where name = '我的群聊' and createUserId = 'ALL') as rel_id,a.userid,a.group_id ,b.targetname,a.isopenfire from
(select userid,group_id,isopenfire from mobile_rongGroup group by userid,group_id,isopenfire) a,(select targetid,targetname from social_IMConversation group by targetid,targetname) b where a.group_id = b.targetid;
```

群聊分组重复：

```sql
delete  from social_imgroup where id <>1 and name = '我的群聊'
```

会话表查群组id：

```sql
select * from social_IMConversation where targetname = '群名';
```

## 名片相关的表

```sql
select * from SOCIAL_IMCHATRESOURCESHARE;
```

## 组织架构查询

查询总部下分所有下级分部（supsubcomid=0）：

```sql
select id,subcompanyname from HrmSubCompany where supsubcomid=0 and (canceled is null or canceled<>1) order by showorder asc , subcompanyname asc;
```

查询总部下分部的部门列表（总部是subcompanyid1=0 and supdepid=0，其他分部的是其他id）：

```sql
select id,departmentname from HrmDepartment where subcompanyid1=0 and (canceled is null or canceled<>1) and supdepid=0 order by showorder asc, departmentname asc;

subcompany：
select id,departmentname from HrmDepartment where subcompanyid1= and (canceled is null or canceled<>1) and supdepid=0 order by showorder asc, departmentname asc
```

查询部门下直接人

```sql
select id,lastname,loginid,messagerurl from HrmResource where departmentid='部门id' and status in(0,1,2,3) order by dsporder;
```

由于上面的supdepid不等于0导致下级部门没有查询出来，emessage上的组织架构没能展示，目前暂时用下面的语句可以修改让其显示出来（supdepid表示多级部门）：

```sql
update HrmDepartment set [supdepid] = 0  where subcompanyid1 in (select id from HrmSubCompany where  supsubcomid=117 and(canceled is null or canceled<>1)) and  (canceled is null or canceled<>1);

oracle：
 update HrmDepartment set supdepid = 0
 where subcompanyid1 in （select id from HrmSubCompany where supsubcomid=0 and
 (canceled is null or canceled<>1)）  and  (canceled is null or canceled<>1) and supdepid is null;
```

## 客户端设置保存

根据userid可以查到每个人的设置：

```sql
select * from Social_IMUserSysConfig a where a.userId = 464;
select * from Social_Pc_ClientSettings;
```

"newMsg"：新消息到达直接弹出窗口；
保存的是json串：

```json
{"download":{"defaultPath":"C:\\Users\\JOJO\\Desktop","isAuto":"false"},"guid":"dfeb2748-b7ac-44f9-a107-bbef689f0f59","login":{"autoLogin":false,"language":"zh"},"mainPanel":{"alwaysQuit":true,"noLongerRemind":false},"msgAndRemind":{"audioSet":{"all":false,"broadcast":false,"group":false,"persion":false},"mailRemind":true,"newMsg":true,"wfRemind":true,"audioSet_all":false},"shortcut":{"openAndHideWin":"ALT+W","screenshot":"CTRL+Q"},"skin":"default"}
```

## 国际化标签

```sql
select * from HtmlLabelInfo a where a.indexid = 18014;
select * from HtmlLabelInfo a where a.labelname like '%禁止%';
```

## 群组消息阅读状态

```sql
根据msgid查询count消息：status=0代表已读，status=1代表未读
select * from social_IMMsgRead where  msgid='' and status=1 order by id asc
```

## 广播数据查询

```sql
--这个是广播内容表
select * from social_broadcast ;

---这个是广播接收者表
select * from social_broadcastreceiver ;

两个表之间通过msgid进行关联,如果想要一个人的广播列表查询不到某一条广播,需要将广播接收者的记录删掉就可以了

步骤:
先用广播内容表查出来对应的内容，对应的msgid，
然后根据msgid查到接收者的记录，然后把接收者的记录删除即可。
```

### emessage最近列表

```sql
delete from social_IMRecentConver where userid = '3945'
```
