# e4界面僵死，没响应

### 问题说明：
这个是针对升级到1606版本的客户的，这个版本新增了一个文件`ecology\WEB-INF\prop\OpenfireModule.properties`，这个文件上配置了访问私有云服务的地址信息，但是该私有云服务尚未部署，所以访问失败。

### 修改方法：
把访问的开关关掉即可。
* **Openfire** : `Openfire=false`(true改为false就可以了)
