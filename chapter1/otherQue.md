## 其他说明

* 1.e-message**多语言**支持需要申请并打上对应的语言包才可以获取支持;
* 2.账户被锁定了无法登陆，解锁办法：在数据库执行一下语句;<br/>
`update HrmResource set passwordlock=0 where loginid='登陆名'`
* 3.消息撤回最大期限设置：<br/>
`ClientSet.maxWithdrawTime = 1200000`
* 4.emessage默认头像，linux环境无法生成中文头像，或者没有默认头像：<br/>
`需要在linux环境上安装宋体字。`