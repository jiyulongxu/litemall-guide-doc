### Litemall 部署指南 第1章 - 下载后端代码并配置

>进入这一章，请确保已经安装好 Git、MySQL、JDK、Maven环境。本章操作均在CentOS7.4服务器上完成。

#### 1.1 下载代码
在/root/目录下创建一个代码文件夹
	
	cd 
	mkdir code

进入code文件夹，使用git检出代码

	cd code
	git clone https://gitee.com/linlinjava/litemall.git

这里使用的码云的路径，litemall在github上也有托管

#### 1.2 配置项目

> 配置项目前需要向微信公众平台(mp.weixin.qq.com)申请一些东西。微信公众平台的appId和appSecret；微信支付平台的mchId、mchKey(32位自己设置的)、application_cert.p12文件。

> 在图片存储上，使用阿里云的OSS对象存储。需要 endpoint、accessKeyId、accessKeySecret、bucketName四个属性。

准备好以上资料后，就编辑Spring Boot的配置文件了。

##### 1.2.1 编辑core
	vim litemall/litemall-core/src/main/resources/application-core.yml

将微信的配置更新上去

	litemall.wx.app-id
	litemall.wx.app-secret
	litemall.wx.mch-id
	litemall.wx.mch-key
	# key-path 是application_cert.p12文件的路径
	litemall.wx.key-path 

回调URL

	https://www.example.com/wx/order/pay-notify

www.example.com 换成自己的接口域名即可

OSS配置

	liteamll.storage.active #这里设置为aliyun
	liteamll.storage.aliyun.endpoint
	liteamll.storage.aliyun.accessKeyId
	liteamll.storage.aliyun.accessKeySecret
	liteamll.storage.aliyun.bucketName

##### 1.2.2 配置MySQL

MySQL配置第一步需要建立MySQL表结构。litemall已经提供了mysql的初始化脚本。在code目录下一次执行以下三条命令即可。中间需要输入三次mysql密码。

	mysql -uroot -p < litemall/litemall-db/sql/litemall_schema.sql
	mysql -uroot -p litemall < litemall/litemall-db/sql/litemall_table.sql
	mysql -uroot -p litemall < litemall/litemall-db/sql/litemall_data.sql

配置application

	vim litemall/litemall-db/src/main/resources/application-db.yml

将spring.datasource.druid.username 改为root

将spring.datasource.druid.password 改为数据库密码1234newpwd!@#ABC



