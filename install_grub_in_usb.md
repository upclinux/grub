# GRUB2 的安装

此处需要 Linux 操作系统和一个 U 盘（FAT32 格式）。为了方便，以 Ubuntu 为例。

由于两种启动模式并不冲突，建议大家把两种模式都安装好。

## UEFI 模式安装

需要安装 `grub-efi-amd64` 软件包。用以下命令安装：

	sudo apt-get install grub-efi-amd64

假设 U 盘已经被挂载到 `/media/user/ABCD-0123`，在 U 盘根目录建立一个名为“efi”的文件夹。输入以下命令安装 GRUB2：

	sudo grub-install --target=x86_64-efi --boot-directory=/media/$user/ABCD-0123/efi --efi-directory=/media/user/ABCD-0123 --removable
	
此时 GRUB 目录为 U 盘 efi 目录里的 `grub` 目录。

## Legacy 模式安装

需要安装 `grub-pc-bin` 软件包。用以下命令安装：

	sudo apt-get install grub-pc-bin
	
假设 U 盘为 `/dev/sdb` （不要加数字），并且已经被挂载到 `/media/user/ABCD-0123`。输入以下命令安装 GRUB2：

	sudo grub-install --target=i386-pc --force --boot-directory=/media/$user/ABCD-0123/grubold /dev/sdb

此时 U 盘并不能拿去启动。需要用一个分区软件将 U 盘分区设置为“活动分区”。以 GParted 为例：

启动 GParted （安装：`sudo apt-get install gparted`），找到 U 盘和 U 盘的分区，右击，选择“管理标识”，并勾选 `boot` 标识。

GRUB 目录为 U 盘根目录下的 `grubold/grub` 目录。

**如果你使用的发行版用的是`grub2-install`，就把对应位置的名字换成grub2即可**
