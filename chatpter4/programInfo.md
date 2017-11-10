# 程序相关代码：

oa文件路径记录：

```txt
客户端相关函数：ecology\social\im\js\im_pc_wev8.js
appkey文件：/ecology/WEB-INF/prop/EMobileRong.properties
过滤器：ecology\WEB-INF\web.xml
组织架构：HrmOrgTree
脚本：ecology\social\im\SocialIMUtil.jsp
群设置文件：SocialDiscussSetting.jsp
图片轮播页面：ecology\social\im\imageReview.jsp
开启emessage功能：ecology\WEB-INF\prop\Messager2.properties
客户端版本：ecology\social\im\resources\emessage.properties
```

浏览器上看：

```txt
/social/im/resources/emessage.properties
```

相关方法：

```txt
显示表情，插入表情：drawExpressionWrap
```

vs-code调试：

```json
{
    "version": "0.2.0",
    "configurations": [{
        "name": "调试主进程",
        "type": "node",
        "request": "launch",
        "cwd": "C:/Users/joe/Desktop/electron_test/",
        "runtimeExecutable": "C:/Users/joe/Desktop/electron_test/electron.exe",
        "program": "C:/Users/joe/Desktop/electron_test/resources/app/main.js"
    }]
}
```

```java
jsp添加日志：
方法一：
<%@page import="weaver.general.BaseBean"%>
BaseBean log = new BaseBean();
log.writeLog("addOrDelGroupBook===========resourceids="+resourceids);

方法二：
<jsp:useBean id="log" class="weaver.general.BaseBean" scope="page" />
log.writeLog("addOrDelGroupBook===========resourceids="+resourceids);


java打日志：
new BaseBean().writeLog("querySql============"+querySql);
```

程序调试总结：

```log
$("#tempchatFloatmenu")：消息体悬浮框div
```

## 顶部快捷栏

```txt
展示页面：social/manager/SocialTopButtonsInner.jsp
保存设置：savefieldbatch1：/ecology8/social/manager/SocialManagerOperation.jsp
select * from Social_Pc_UrlIcons a;


/ecology8/social/im/SocialIMPcModels.jsp
（设置为-1会报错，这个功能是云盘）
update Social_Pc_UrlIcons set icotype = -1 where linkuri = '/rdeploy/chatproject/doc/index.jsp
```

## 页面设置上传附件大小

```log
页面地址：social/manager/SocialAppSettingCommon.jsp

根据表查询设置：
select * from Social_Pc_ClientSettings where fromtype = '1';
一共有两项，maxGroupMems 群组人数上限， maxAccUploadSize 上传附件大小限制

可以通过数据库直接更新该字段：
update Social_Pc_ClientSettings set keyvalue = '2048' where keytitle = 'maxAccUploadSize';

提交保存:SocialManagerOperation.jsp?method=basesetting&fromtype=1
```

## 单点登录

```SQL
select sysid,name from outter_sys;
select * from Social_Pc_UrlIcons where icotype = '1' order by showindex
```