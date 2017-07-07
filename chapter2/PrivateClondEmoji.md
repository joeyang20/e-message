# 私有云发送表情乱码

### 解决办法：

* 在**e-message/conf**目录下新增文件**encoding.properties**，内容如下：<br/>
`encoding=gbk`
* 然后重启私有云的服务即可解决问题
