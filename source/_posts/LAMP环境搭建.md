title: LAMP环境搭建
date: 2016-05-24 06:10:53
tags:
---

## Linux软件安装
1. 什么是开放源码、编译程序与可执行文件
	* 可执行文件：Linux系统上真正识别的可执行文件其实是二进制文件，该文件需要有x可执行权限
	* 编译程序：将人类看的程序语言翻译为机器看得懂的语言。例如在Linux上标准的c语言编译程序为gcc
	* 开放源码：程序代码，写给人类看的程序语言
	* 判断一个文件是否为二进制 file name会显示（ELF 32-bit LSB executable）
2. RPM,全名Redhat Package Manager<!-- more -->
	* RPM是以一种数据库记录的方式来将你所需要的软件安装到你的Linux系统的一套管理机制
	* rpm包格式(例如rp-pppoe-3.1-5.i386.rpm)
	{% codeblock %}
	rp-pppoe-      3.1          -      5           .i386         .rpm
	 软件名称  软件的版本信息      发布的次数   适合的硬件平台   扩展名
	{% endcodeblock %}
    * rpm相关命令
	{% codeblock %}
	rpm –ivh 包全名
	选项：
	    -i（install）	安装
	    -v（verbose）	显示详细信息
	    -h（hash）	显示进度
	    --nodeps	不检测依赖性

	rpm -q 包名
	查询包是否安装

	rpm -e 包名
	选项：
		-e（erase） 卸载
	{% endcodeblock %}
	* rz、sz命令的安装方法
	yum安装不成功时可以下载rpm包来安装[lrzsz-0.12.20-22.1.x86_64.rpm](http://yun.baidu.com/share/link?shareid=355587411&uk=3934253933)
	* rpm属性依赖的解决方式：yum

## 光盘yum源搭建和yum命令
1. 挂载光盘
	{% codeblock %}
	mount /dev/cdrom /mnt/cdrom/
	{% endcodeblock %}
2. 让网络yum源文件失效
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

