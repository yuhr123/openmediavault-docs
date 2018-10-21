使用 ISO 镜像安装
###############################

制作安装器
------------------
	对于 x86 架构的设备，你可以使用 `etcher <https://etcher.io/>`_ 或 linux 的 dd 
	命令直接将 ISO 镜像写入 U 盘::

	$ sudo dd if=xxx.iso of=/dev/sdX bs=4096

	如果你有 CD-DVD 光驱，可以刻录 ISO 镜像光盘并从 CD 或 DVD 引导启动。

引导安装器
------------------
	对于 x86 架构的 PC 主机，请参照计算机或主板说明书，开机引导进入 BIOS 设置，选择从 USB
	或 CD 引导启动。

安装器
---------
	当前 ISO 安装器对安装过程的交互做了进一步的精简，你需要选择地区、语言并设置 ``root`` 
	密码。安装器会将系统安装在第一个可用磁盘。系统会在安装完成后重启，请在安装完成后移除安装盘
	并从系统盘引导启动，然后就可以重新连接之前断开的数据盘了。

	.. figure:: /_static/images/install_via_iso/install_1.png
	.. figure:: /_static/images/install_via_iso/install_2.png
	.. figure:: /_static/images/install_via_iso/install_3.png
	.. figure:: /_static/images/install_via_iso/install_4.png
	.. figure:: /_static/images/install_via_iso/install_5.png
	.. figure:: /_static/images/install_via_iso/install_6.png
	.. figure:: /_static/images/install_via_iso/install_7.png
	.. figure:: /_static/images/install_via_iso/install_8.png
	.. figure:: /_static/images/install_via_iso/install_9.png
	.. figure:: /_static/images/install_via_iso/install_10.png
	.. figure:: /_static/images/install_via_iso/install_11.png
	.. figure:: /_static/images/install_via_iso/install_12.png
	.. figure:: /_static/images/install_via_iso/install_13.png
	.. figure:: /_static/images/install_via_iso/install_14.png
	.. figure:: /_static/images/install_via_iso/install_15.png
	.. figure:: /_static/images/install_via_iso/install_16.png
	.. figure:: /_static/images/install_via_iso/install_17.png
	.. figure:: /_static/images/install_via_iso/install_18.png
	.. figure:: /_static/images/install_via_iso/install_19.png

故障排除
---------------

发生 `Unable to install GRUB in /dev/sda` 错误。
	这种情况可以执行以下步骤：

	- Select `Continue` in this window and also on the next which says
	  `Installation step failed`.
	- In the Debian installer main menu (which should have popped up by now),
	  select `Execute a shell` and then `Continue`.
	- Execute the following commands::

		# Chroot.
		chroot /target
		# Replace [a-z] with the drive you want to install grub to.
		# This is normally the drive you've selected to install OpenMediaVault on.
		grub-install /dev/sd[a-z]
		# Update GRUB.
		update-grub
		# Exit chroot.
		exit
		# Exit shell.
		exit

	- Select `Continue without boot loader` in the Debian installer main menu and
	  then `Continue`.
	- It should now continue the installation successfully.
