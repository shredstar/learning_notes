# X86汇编语言从实模式到保护模式
- 李忠、王晓波、余洁
- http://blog.163.com/leechung@126
- leechung@126.com

## 第1部分 预备知识

### C01 十六进制计数法 

### C03 汇编语言和汇编软件

安装nasm的X86版。
- 编译命令如下：
	```
	nasm -f bin filename.asm -o filename.bin
	```
	- -f 参数的作用是指定输出文件的格式（Format），```-f bin```就是要求NASM生成的文件只包含“纯二进制内容”。 
	- -o 参数制定输出的文件名

 

## 第2部分 实模式

## 第3部分 保护模式

### C08 硬盘和显卡的访问与控制
2/13/2020 5:40:44 PM 

## Resource
[勘误表](http://blog.163.com/leechung@126/blog/static/70525507201301803044445/)

[穿越计算机的迷雾](http://blog.163.com/leechung@126/blog/static/70525507201011111024388/)

[win10搭建x86汇编编程环境](https://blog.csdn.net/sinat_38788608/article/details/95915498)

[《x86汇编语言:从实模式到保护模式》 前几章配置环境说明总结](https://blog.csdn.net/OneTrianee/article/details/80410816)

[《x86汇编语言：从实模式到保护模式》-官网](http://www.lizhongc.com/x86asm/serv.asp)

[win10显示中文乱码，应该如何设置](https://www.zhihu.com/question/34761050)

[How to Create and Run Virtual Machines With Hyper-V](https://www.howtogeek.com/196158/how-to-create-and-run-virtual-machines-with-hyper-v/)

[虚拟磁盘格式简单说明](https://www.cnblogs.com/jinanxiaolaohu/p/9246480.html)

[镜像文件格式](https://www.jianshu.com/p/47a4b1c2f695)
- RAW：RAW即常说的裸格式，它其实就是没有格式，最大的特点就是简单，数据写入什么就是什么，不做任何修饰，所以再性能方面很不错，甚至不需要启动这个镜像的虚拟机，只需要文件挂载即可直接读写内部数据。并且由于RAW格式简单，因此RAW和其他格式之间的转换也更容易。在KVM/XEN的虚拟化环境下，有很多使用RAW格式的虚拟机
- qcow2：qcow（Qemu copy-on-write format 2）的升级版本，它是QEMU的CopyOn Write特性的磁盘格式，主要特性是磁盘文件大小可以随着数据的增长而增长。譬如创建一个10GB的虚拟机，实际虚拟机内部只用了5GB，那么初始的qcow2磁盘文件大小就是5GB。与RAW相比，使用这种格式可以节省一部分空间资源。最早是cow，后来被qcow取代。有点很多：
	- 更小的存储空间，即使是不支持holes的文件系统也可以（这下du -h和ls -lh看到的就一样了）
	- Copy-on-write support, where the image only represents changes made to an underlying disk image（这个特性SUN ZFS表现的淋漓尽致）
	- 支持多个snapshot，对历史snapshot进行管理
	- 支持zlib的磁盘压缩
	- 支持AES的加密
- VHD：一种通用的磁盘格式。微软公司的Virtual PC和Hyper-V使用的就是VHD格式。VirtualBox也提供了对VHD的支持。如果要在OpenStack上使用Hyper-V的虚拟化，就应该上传VHD格式的镜像文件。后期新增vhdx格式，有了更好的性能和参数。
- VMDK：VMware创建的一个虚拟机磁盘格式，目前也是一个开放的通用格式，除了VMware自家的产品外，QEMU和VirtualBox也提供了对VMDK格式的支持。一般情况下，单个虚拟机的最大磁盘是2T。超过2T的虚拟机无法制作快照。
- VDI：Oracle公司的VirtualBox虚拟软件所使用的格式
- AKI、ARI、AMI：Amazon公司的AWS所使用的镜像格 

[About Linux](https://developer.ibm.com/technologies/linux/)