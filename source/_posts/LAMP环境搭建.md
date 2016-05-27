title: LAMP环境搭建
date: 2016-05-24 06:10:53
tags:
---

## 光盘yum源搭建和yum命令
1. 挂载光盘
	{% codeblock %}
	mount /dev/cdrom /mnt/cdrom/
	{% endcodeblock %}
2. 让网络yum源文件失效<!-- more -->
	{% codeblock %}
	cd /etc/yum.repos.d/
	mv CentOS-Base.repo CentOS-Base.repo.bak
	mv CentOS-Debuginfo.repo CentOS-Debuginfo.repo.bak
	mv CentOS-Vault.repo CentOS-Vault.repo.bak
	{% endcodeblock %}
    mv的功能表示剪切文件、改名
3. 修改光盘yum源文件
	* vim CentOS-Media.repo
	* 设置baseurl=file:///mnt/cdrom，并且注释掉下面两个不存在的地址
	* 把enabled=0改为enabled=1，让这个yum源配置文件生效
4. 常用yum命令
	{% codeblock %}
	yum list //查询所有可用软件包列表
	yum search 关键字 //搜索服务器上所有和关键字相关的包
	yum –y install 包名 //安装，-y表示自动回答yes
	yum -y remove 包名 //卸载
	{% endcodeblock %}

   

