## 其他说明

* 1.e-message**多语言**支持需要申请并打上对应的语言包才可以获取支持;
* 2.账户被锁定了无法登陆，解锁办法：在数据库执行一下语句;<br/>
```
update HrmResource set passwordlock=0 where loginid='登陆名'
```
* 3.消息撤回最大期限设置：<br/>
```
ClientSet.maxWithdrawTime = 1200000
```
* 4.emessage默认头像，linux环境无法生成中文头像，或者没有默认头像：<br/>
`需要在linux环境上安装宋体字。`
* 5.修改上传附件大小限制（默认是300m，可通过数据库修改，单位是m）
```
update Social_Pc_ClientSettings set keyvalue = 1024 where fromtype = '1' and keytitle = 'maxAccUploadSize';
```
* 6.oa文件路径记录：
```
客户端相关函数：ecology\social\im\js\im_pc_wev8.js
appkey文件：/ecology/WEB-INF/prop/EMobileRong.properties
过滤器：ecology\WEB-INF\web.xml
```
* 7.修改oa链接已断开提示：<br/>
修改文件：ecology\social\im\js\im_pc_wev8.js<br/>
位置如下图：<br/>
![修改位置](/image/c1/修改客户端连接断开提醒.png "Title")

