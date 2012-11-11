---
layout: page
title: 关于grub
category: 技术
---
<h2>{{page.title}}</h2>
<p>{{page.date | date_to_string}}</p>
关于grub的修复：

问题：
	acer4750G的机子，win7的系统。制作U盘启动盘，安装64位ubuntu12.04之后，无启
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

	4.	mount -o rw /dev/sda9 /boot 	#挂载 /boot 分区，若没有分此区，跳过

	5.	grub-install /dev/sda		#此处一定是 sda 没有任何后缀的数字，
						 是整个硬盘下的意思
	6.	update-grub
	
	重启进入，应该会有启动项了；

参考文章：<a href="http://www.zhouwenyi.com/node/6756/">使用Ubuntu Live CD修复Grub引导</a>

补充1：
	
	进入ubuntu12.04之后，当时没注意，手痒，点了个检查更新，所以重启下次进
	入ubuntu12.04时，报错，所以只能，重复上面步骤，原因是更新把grub又更新
	成了grub2;
	建议大家进入之后，首先关闭检查更新，就在右边最上方面板的用户注销那块儿
	，在检查更新的属性里改为 "从不"；
	
补充2：
	
	如果有人安装之后，进入时连win7都进不了，之间显示grub resuce> 方法如下：
	用U盘启动盘进入ubuntu12.04，打开shell，输入命令如下：
	1.	sudo apt-get remove grub-efi-amd64	#移除grub-efi
	2.	sudo apt-get install grub-pc		#安装普通grub
	3.	sudo mount /dev/sda9 /mnt		#挂载 /boot 分区，
							 若没有，挂载你的 /分区
	4.	sudo grub-install --root-directory=/mnt /dev/sda 
	尝试重启；

参考文章：<a href="http://datamining.xmu.edu.cn/bbs/forum.php?mod=viewthread&tid=624/">解决Grub Rescue: invalid arch independent ELF magic问题</a>

补充3：
	
	主题：关于卸载linux
	描述：
	其实我当时的问题主要在于以前装过ubuntu10.04,又没有正常卸载，留下了grub的
	遗留问题；没有概念和不会是完全不一样滴，没有概念 ==> 不会 、 不会 =/=> 没有概念，
	我是前者，完全的以为格式化就完事了；
	方法：
	卸载linux步骤：
	打开shell,命令如下：
		sudo dd if=/usr/lib/sys/mbr.bin of=/dev/sda

参考文章：<a href="http://blog.csdn.net/majestyhao/article/details/7913429/">一个及其简单的卸载linux的方法</a>