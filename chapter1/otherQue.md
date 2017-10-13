# 其他说明

* 1.e-message**多语言**支持需要申请并打上对应的语言包才可以获取支持;
* 2.账户被锁定了无法登陆，解锁办法：在数据库执行一下语句;

```sql
update HrmResource set passwordlock=0 where loginid='登陆名'
```

* 3.消息撤回最大期限设置：

```sql
ClientSet.maxWithdrawTime = 1200000
```

* 4.emessage默认头像，linux环境无法生成中文头像，或者没有默认头像：

`需要在linux环境上安装宋体字。`

* 5.修改上传附件大小限制（默认是300m，可通过数据库修改，单位是m）

```sql
update Social_Pc_ClientSettings set keyvalue = 1024 where fromtype = '1' and keytitle = 'maxAccUploadSize';
```

7.修改oa链接已断开提示：

修改文件：ecology\social\im\js\im_pc_wev8.js
位置如下图：
![修改位置](/image/c1/修改客户端连接断开提醒.png "Title")

8.客户端快捷键
win版本

```txt
撤销  Ctrl+Z
重做  Shift+Ctrl+Z
剪切  Ctrl+X
复制  Ctrl+C
全选  Ctrl+A
清理缓存 Ctrl+R
切换全屏 F11
最小化 Ctrl+M
关闭 Ctrl+W
```

mac版本

```txt
撤销  Command+Z
重做  Shift+Command+Z
剪切  Command+X
复制  Command+C
全选  Command+A
清理缓存 Command+R
切换全屏 Ctrl+Command+F
最小化 Command+M
关闭 Command+W
隐藏 Command+H
隐藏其它 Command+Alt+H
退出 Command+Q
```

9.检查文件系统语言版本

```sql
select language, activable from syslanguage where activable = 1 and id = 7;
(7(简体中文),8(英文),9(繁体中文))
```

10.手机端检查连接消息云:

除了检查5222端口的访问，可以通过服务接口的访问来确认数据：

```html
http://office.whit.edu.cn:89/client.do?method=login&loginid=jcx&password=1
```

```json
{"openfaceanalyse":"0","sessionkey":"abcjsvvNDvMpKenObaP6v","hrmorgshow":"true","hasBroadCast":null,"rongAppKey":"8w7jv4qb7ucqy","commonGroupshow":"true","mysubordinateshow":"true","version":"6.5","openfireDomain":"","ryudidNew":"ZzQLNDI9","headpic":"\/messager\/images\/icon_m_wev8.jpg","openfireHost":"office.whit.edu.cn","openfireModule":"true","navigation":[{"id":"1","default":"1","ulogo_url":null,"logo_url":null,"url":"","displayname":"消息"},{"id":"2","default":"0","ulogo_url":null,"logo_url":null,"url":"","displayname":"应用"},{"id":"3","default":"0","ulogo_url":null,"logo_url":null,"url":"","displayname":"通讯录"},{"id":"4","default":"0","ulogo_url":null,"logo_url":null,"url":"","displayname":"我"}],"sameDepartmentshow":"true","createworkflow":"1","groupChatshow":"true","allPeopleshow":"true","creategroupchat":"1"}
```