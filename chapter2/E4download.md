# oa主页无法下载最新e4软件

### 1.确认是否升级到了e4，就是检验e-message的版本
##### 具体操作如下：打开项目后台*/ecology/social/im/resources/emessage.properties*这个文件，确认version字段的信息

* a.如果确认系统已经申请升级到e4了，但是里面的verison=3.8，需要把version改为4.0,
* b.只要确保改为4.0即可，其他参数可以先不用管

操作完成后重启服务，在测试一下。

### 2.如果上述操作无法解决问题，需要检验后台更新页面是否正确
##### 具体操作如下：打开项目目录 *ecology\messager\installm3*，查看是否存在*emessageproduce.jsp*和*emessageproduce3.jsp*文件

* *emessageproduce.jsp* : 新版e4的下载页面，更新后会把原来的e3的下载页面改为下面的名称
* *emessageproduce3.jsp* : 旧版e3的下载页面

如果两个页面都存在，那代表文件更新没有错误，如果只存在其中一个文件，代表出错，需要检查升级包的内容或者向总部配置组请求更新该文件
