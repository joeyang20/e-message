# pc端无法查看消息记录
* 1.消息记录调用方法`ChatUtil.showChatRecord(this)`,
打开页面`/ecology/social/im/SocialIMChatRecord.jsp`，

`select r.* from (     select my_table.*, rownum as my_rownum from (    select tableA.*,rownum  as r from (   select id,fromUserId,targetId,targetType,GroupId,classname,msgContent,extra,type,imageUri,dateTime from HistoryMsg where  ((fromuserid='646' and targetid='125') or (fromuserid='125' and targetid='646')) and classname not in ('RC:VcMsg', 'RC:LBSMsg', 'RC:DizNtf')  order by datetime desc,id desc) tableA  ) my_table where r < 11 and r>0) r`
