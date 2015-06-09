grub.cfg
===

基于 GRUB2 的万能启动 U 盘。支持 Windows（PE/安装盘）、多种 Linux 发行版。

# 文件

配置文件分两种，看那两个文件名就知道了。

Legacy 版本的由于条件有限，没有测试完全，大家自己测试吧，不对的地方自己修改，欢迎上传修改版。

*（此处需要更正。后面有详细解释。）grub_efi.cfg放在/EFI/grub/下，grub_legacy.cfg放在/grubold/grub/下*

使用时改名为 grub.cfg

有的配置实在很难找，本人也是各种谷歌，可算弄了份能用的……
如果有镜像文件对应不上的，请自行修改文件名。大家可以根据自己的需要自行修改内部的功能。

# GRUB2 的安装

此处需要 Linux 操作系统和一个 U 盘（FAT32 格式）。为了方便，以 Ubuntu 为例。

由于两种启动模式并不冲突，建议大家把两种模式都安装好。

## UEFI 模式安装

需要安装 `grub-efi-amd64` 软件包。用以下命令安装：

	sudo apt-get install grub-efi-amd64

假设 U 盘已经被挂载到 `/media/user/ABCD-0123`，在 U 盘根目录建立一个名为“efi”的文件夹。输入以下命令安装 GRUB2：

	sudo grub-install --target=x86_64-efi --boot-directory=/media/$user/ABCD-0123/efi --efi-directory=/media/user/ABCD-0123 --removable
	
此时 GRUB 目录为 U 盘 efi 目录里的 grub 目录。

## Legacy 模式安装

需要安装 `grub-pc-bin` 软件包。用以下命令安装：

	sudo apt-get install grub-pc-bin
	
假设 U 盘为 `/dev/sdb` （不要加数字），并且已经被挂载到 `/media/user/ABCD-0123`。输入以下命令安装 GRUB2：

	sudo grub-install --target=i386-pc --force --boot-directory=/media/$user/ABCD-0123/grubold /dev/sdb

此时 U 盘并不能拿去启动。需要用一个分区软件将 U 盘分区设置为“活动分区”。以 GParted 为例：

启动 GParted （安装：`sudo apt-get install gparted`），找到 U 盘和 U 盘的分区，右击，选择“管理标识”，并勾选 `boot` 标识。

GRUB 目录为 U 盘根目录下的 grub 目录。将 grub_legacy.cfg 复制到里面并更名为 grub.cfg 即可使用。
