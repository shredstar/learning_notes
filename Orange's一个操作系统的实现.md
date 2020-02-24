-sys# 01 马上动手写一个最小的“ 操作系统”

- **准备工作**  
  1.在host-win安装x86模拟器**bochs**, 同时就用了工具**bximage**  
  2.安装虚拟化平台（Hypvisor）**qemu**
  3.利用qemu创建虚拟机，安装**Ubuntu** 
		+ 虚拟机信息
			- hostname: ubuntu01
			- username：xing
			- passwd: Ryqz050924@os
  4.在vm-linux中安装汇编编译器**NASM**（Netwide Assembler），真正是为了编译   
  

- **知识点** 
  - 利用软盘启动系统，引导扇区位于0面0磁道0扇区，标志：以0xAA55结束  
      + _疑问：引导程序为什么要被加载到0x7C00处？_  

- **关键代码** 
 
```nasm
;%define _BOOT_DEBUG_	; 制作 Boot Sector 时一定将此行注释掉!			
	; 去掉此行注释后可做成.COM文件易于调试:			
	; nasm Boot.asm -o Boot.com 
%ifdef  _BOOT_DEBUG_	
	org  0100h		; 调试状态, 做成 .COM 文件, 可调试
%else	
	org  07c00h		; BIOS 将把 Boot Sector 加载到 0:7C00 处
%endif	

	mov	ax, cs	
	mov	es, ax			; 记录代码段地址	
	call DispStr		; 调用显示字符串例程	
	jmp	$				; 无限循环

DispStr:	
	mov	ax, BootMessage	
	mov	bp, ax		; ES:BP = 字符串地址：段+偏移，int 10h显示字符串时，必须提供上述地址	
	mov	cx, 16		; CX = 字符串串长度	
	mov	ax, 01301h	; AH = 13,  AL = 01h，调用10h中断时，AH=13h表示输出字符串；AL=01h表示Update cursor after writing	
	;mov bx, 000ch	; 页号为0(BH = 0) 黑底红字(BL = 0Ch,高亮)	
	mov bx, 0071h	; 页号为0(BH = 0) 白底蓝字(BL = 71h)	
	mov	dl, 20		; 显示位置，dh - 行；dl - 列	
	int	10h			; int 10h，调用bios的10h中断（显示信息）	
	ret				; 子程序返回指令

BootMessage: db	"Hello, OS world!“
	times 	510-($-$$)	db	0 ; 填充剩下的空间，使生成的二进制代码恰好为512字节（数组）
	dw 	0xaa55		 ; 结束标志（数组）
```

# 02 搭建你的工作环境
- host-win：用notepad++看/写代码，包括看二进制代码
- host-win：用bximage生成磁盘镜像
- vm-linux：调用make、nasm、GCC等工具对代码进行编译，利用dd等工具操作磁盘镜像
- host-win：利用bochs运行、调试操作系统

# 03 保护模式（Protect Mode）

## 3.1 认识保护模式
- 一致代码段： 程序转移目标是一个特权级更高的一致代码段，当前的特权级会被延续下去 - 特权级保持不变，并且可以继续执行？
- 非一致代码段： 程序转移目标是一个特权级更高的非一致代码段，会引起常规保护错误（General-protection exception）
- 为什么高优先级代码不能访问低优先级代码？而高优先级数据可以访问低优先级数据？

- 描述符Descriptor，到底有什么用？
- 选择子Selector，到底是什么？

## 3.2 保护模式进阶
gdtr，ldtr到底是啥？


### 3.2.1 海阔凭鱼跃
5M基地址怎么表示？

### 3.2.2 LDT（Local Discriptor Table)

### 3.2.3 特权级概述
- 3种特权等级定义
	- CPL
	- DPL
	- RPL
- 代码段跳转方法，程序控制转移的发生，可以是由指令jmp、call、ret、sysenter、sysexit、int n或iret引起的，也可以由中断和异常机制引起。
	使用jmp或call指令可以实现下列4种转移：
	1. 目标操作数包含目标代码段的段选择子。 
	2. 目标操作数指向一个包含目标代码段选择子的调用门描述符。 
	3. 目标操作数指向一个包含目标代码段选择子的TSS。 
	4. 目标操作数指向一个任务门，这个任务门指向一个包含目标代码段选择子的TSS。 
	这4种方式可以看做是两大类，一类是通过jmp和call的直接转移（上述第1种），另一类是通过某个描述符的间接转移（上述第2、3、4种）。

### 3.2.4 特权级转移
- 长跳转 vs. 短跳转
	- 长跳转：段间跳转
	- 短跳转：段内跳转
- TSS（Task-State Segment）
	- 
## 3.3 页式存储
- 所谓“页”，就是一块内存

### 3.3.1 分页机制概述

### 3.3.2 编写代码启动分页机制
- cld
- lodsb
- cr系列寄存器
	- cr3，PDBR，Page-Directory Base Register
- TLB - Translation Lookaside Buffer

### 3.3.3 PDE和PTE
PDE和PTE的长度都是32 bit，4 byte。其中控制位都是12 bit，地址长度都是20 bit
一个PDE对应一个PT。一个PT有1024个PTE。一个PTE对应一块4K内存。所以一个PT对应4M内存

### 3.3.4 cr3
cr3又叫Page Directory Base Register，其高20位是页目录表的首地址的高20位。而页目录表的首地址的低12位全是0。其实cr3就是存放的页目录表的首地址。

PDE中的页表基址（Page Table Base Address）以及PTE中的页基址（Page Base Address）也是低12位全是0。这表明地址分配的时候，是以4K为单位分的。PDE和PTE是4K对齐的。

### 3.3.5 回头看代码
内存页目录及页表结构
- PD有1024个PDE
- 一个PDE对应一个PT
- 一个PT有1024个PTE
- 一个PTE对应4K内存

上述结构下，可以存放页目录的内存为4K，存放页表的内存为4M，可以管理的内存线性地址为4G。

### 3.3.6 克勤克俭用内存





# 04 让操作系统走进保护模式


# 05 内核雏形

## 5.1 在Linux下用汇编写Hello World

## 5.2 再进一步，汇编和C同步使用

## 5.3 ELF（Executable and Linkable Format)




# A 附录
## A01 X86 CPU寄存器说明

- 通用寄存器reg  

序号 | 名称 | 作用 | 说明 |
--- | --- | --- | --- |
1 | ax | 累加器 | - |
2 | bx | 基地址寄存器 | - |
3 | cx | 计数寄存器 | - |
4 | dx | 数据寄存器 | - |
5 | sp | 堆栈指针寄存器 | 存放栈顶指针 |
6 | bp | 基地址指针寄存器 | 保存局部变量 |
7 | si | 源地址寄存器 | 存放内存地址 |
8 | di | 目的地址寄存器 | 存放内存地址 |
9 | ip | 指令地址寄存器 | 偏移地址。 |

- 段寄存器sreg

序号 | 名称 | 作用 | 说明 |
--- | --- | --- | --- |
1 | cs | 代码段基地址寄存器 | ```cs:ip```，用于指示当前指令地址 |
2 | ds | 数据段基地址寄存器 | - |
3 | ss | 堆栈段基地址寄存器 | ```ss:sp``` - 栈顶元素地址 |
4 | es | 附加段基地址寄存器 | 作用于ds相当，```es:bp```，某些中断要求的地址 |
5 | gs | 图形数据段基地址寄存器 | 图形数据起始地址 |

- 其他寄存器

序号 | 名称 | 作用 | 说明 |
--- | --- | --- | --- |
1 | gdtr | - | - | 
2 | cr0 | - | - |
3 | cr3 | - | - |

## A02 NASM相关说明
- 语法说明
  1. 在NASM中，标签和变量名等价，都是内存地址
  2. 方括号[]：[标签/变量名]表示内存地址中的内容
  ```nasm
	mov ax, foo		; 将foo代表的地址赋给ax
	foo dw 1		; 在foo代表的地址中存放1
	mov ax, [foo]	; 将1赋给ax
  ```
  3. $ - 表示当前地址；$$ - 表示当前段（section/segment）的起始地址
  4. ```ret``` - 子程序返回指令
  5. 数组定义
  6. 宏定义与调用
  7. ALIGN
  8. lgdt
  9. cli
  10. cld
  11. lodsb
  12. movzx

- 编译与执行
	- 生成纯二进制文件（Raw Binary File或Flat-form Binary File）
	```nasm loader.asm -o loader.bin```
	- 编译Linux下的目标文件
	```nasm -f elf loader.asm```
	- 生成Linux下的可执行文件
	```ld -m elf_i386 -s -o loader loader.o```

## A03 bochs相关说明
- 配置bochs文件```.bochsrc / bochsrc / bochsrc.bxrc```，以下两行很重要：
	```
	# filename of ROM images
	romimage: file=D:\Onebox\03Learning\02BuildingOS\05misc\BIOS-bochs-latest
	vgaromimage: file=D:\Onebox\03Learning\02BuildingOS\05misc\VGABIOS-elpin-2.40
	``` 
 	配置好```bochsrc```后，直接在对应目录中，输入```bochs```命令可以启动bochs，输入```bochsdbg```，启动bochs，进入Debug状态

- 创建磁盘镜像
	```bximage```

- ```bochsdbg```调试命令列表
	**说明：从bochs2.3.5以后，就没有```dump_cpu```命令了。**

行为 | 指令 | 举例 |
--- | --- | --- |
在物理地址设施断点 | ```b addr``` | ```b 0x7c00``` |
显示所有断点信息 | ```info break``` | ```info break``` |
继续执行，直到遇上断点 | ```c``` | ```c``` |
单步执行 | ```s``` | ```s``` |
单步执行（遇到函数则跳过） | ```n``` | ```n``` |
查看寄存器信息 | ```info cpu```,  ```r```,  ```fp```, ```srge```, ```creg``` | ```info cpu```,  ```r```,  ```fp```, ```srge```, ```creg``` |
查看堆栈 | ```print-stack``` | ```print-stack``` |
查看内存物理地址内容 | ```xp /nuf addr``` | ```xp /40bx 0x9013e``` |
查看线性地址内容 | ```x /nuf addr``` | ```x /40bx 0x13e``` |
反汇编一段内存 | ```u start e``` | ```u 0x30400 0x3040D``` |
反汇编执行的每一条指令 | ```trace-on``` | ```trace-on``` |
每执行一条指令就打印CPU信息 | ```trace-reg``` | ```trace-reg on``` |

##A04 qemu相关说明
- 生成40G硬盘镜像
```qemu-img create hd.img 4000M```

- 查看某类CPU支持的具体的机器类型
```qemu-system-aarch64 -machine help```

- 利用iso镜像文件，生成VM。注意，VM的内存至少要有2G
```qemu-system-i386 -hda hd.img -boot d -cdrom ubuntu-16.04.6-server-.iso -m 2048```

- 运行VM
```qemu-system-i386 hd.img -m 2048```

- 网络信息
	- host IP：```10.0.2.2```
	- vm IP： ```10.0.2.15```

##A05 linux相关说明
- 加载及卸载windows下的目录
```sudo mount.cifs //10.0.2.2/02BuildingOS /mnt/win/ -o user=uname,pass=wd,domain=DNAME```	
```sudo umount /mnt/win/```

- 加载及卸载软盘镜像
```sudo mount -o loop a.img /mnt/floppy/```
```sudo umount /mnt/floppy/```

- 在虚拟磁盘镜像中写入文件
	```dd if=boot.bin of=a.img bs=512 count=1 conv=notrunc```
