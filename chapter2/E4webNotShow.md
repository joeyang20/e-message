# web端无法展示e-message操作面板

### 1.首先需要确定是否打开了e-message的功能（该配置文件已经作废）
##### 具体操作如下：打开项目后台*/ecology/WEB-INF/prop/weaverIMconfig.properties*这个文件
* a.如果是"isuse=1"，则代表e-message现在是启用状态
* b.如果是"isuse=0"，则代表e-message现在是禁用状态

### 2.确认是否升级到了e4，就是检验e-message的版本，e3是无法打开web面板的

##### 具体操作如下：打开项目后台*/ecology/social/im/resources/emessage.properties*这个文件，确认version字段的信息

* a.如果确认系统已经申请升级到e4了，但是里面的verison=3.8，需要把version改为4.0,
* b.只要确保改为4.0即可，其他参数可以先不用管

### 3.然后需要确定是否开启即时通讯
##### 具体操作如下：打开项目后台*/ecology/WEB-INF/prop/Messager2.properties*这个文件
* a.如果是"IsUseEMessager=1"，则代表e-message现在是启用状态
* b.如果是"IsUseEMessager=0"，则代表e-message现在是禁用状态

### 4.web端和pc端使用习惯说明
* a.web端和pc端存在冲突,不能多端同时登陆,登陆web端需确认pc端已经退出或者注销
* b.使用浏览器也需要注意，目前仅支持ie10及以上版本浏览器和chrome内核的浏览器使用
