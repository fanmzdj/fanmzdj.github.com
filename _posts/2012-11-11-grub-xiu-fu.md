---
layout: page
title: 关于grub
category: 技术
---
<h2>{{page.title}}</h2>
<p>{{page.date | date_to_string}}</p>
关于grub的修复：

问题：
	acer4750G的机子，win7的系统。制作U盘启动盘，安装ubuntu12.04之后，无启
	动项；


原因：
	从ubuntu10.04到ubuntu12.04，内核工具从grub也升级到了grub2,因为acer主板
	的原因，好像是grub2与EIF接口的不兼容问题；

方法：
	用U盘启动盘进入ubuntu12.04，将grub2卸载，安装grub，具体步骤如下：
	以我的机子为例，我的ubuntu12.04安装时，分区 / 和 /boot,分别挂载在 
	sda8 和 sda9.
	打开shell，输入以下命令：

	1.	sudo -i		#进入root用户

	2.	lsblk		#查看磁盘分区列表，记得当时的分区大小，找到对应的 / 
				 和 /boot 挂载区

	3.	mount -o rw /dev/sda8 / 	#挂载 / 分区

	4.	mount -o rw /dev/sda9 /boot #挂载 /boot 分区

	5.	grub-install /dev/sda		#此处一定是 sda 没有任何后缀的数字，
						 是整个硬盘下的意思
	6.	update-grub
	
	重启进入，应该会有启动项了；
	
补充：
	
	进入ubuntu12.04之后，当时没注意，手痒，点了个检查更新，所以重启下次进
	入ubuntu12.04时，报错，所以只能，重复上面步骤，原因是更新把grub又更新
	成了grub2;
	建议大家进入之后，首先关闭检查更新，就在右边最上方面板的用户注销那块儿
	，在检查更新的属性里改为 "从不"；