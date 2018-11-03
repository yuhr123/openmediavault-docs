FAQ 常见问题
===================

**用户最常碰到的问题**

什么是 OMV？
	OMV 是 |omv| 的缩写。

|omv| 是 FreeNAS 的分支吗？
	不是

|omv| 是否有我的硬件驱动？
	All module drivers are provided by the Debian standard kernel of oldstable
	release 8.9 (aka Jessie). This distribution ships with kernel 3.16 by
	default. Optionally is possible to install the backport kernel 4.9. If
	hardware is supported under Debian Jessie then is supported under |omv|.
	The Jessie backport kernel 4.9 is the default kernel used by Stretch
	(Debian 9.3) at the moment, so it provides support for newer hardware.

|omv| 可以安装在 U 盘上吗？
	Yes, but the installation does not have any optimizations to reduce writes
	into the OS disk. The usb media will most likely start failing within a
	few weeks of usage. Most common symptom is basic command execution does
	not work, denied login, etc. More information `here <https://forum.openmediavault.org/index.php/Thread/6438-Tutorial-Experimental-Third-party-Plugin-available-Reducing-OMV-s-disk-writes-al/>`_.

我可以给非管理员访问 Web 管理面板的权限吗？
	No. By default non-admin users can only access their account profile, they can change
	password and their email address if the admin has allowed changes on their account.
	However the current |webui| framework is designed for developers to create plugins where
	they can give limited or full access to non-admin users to their plugin. An example is in the
	`openvpn plugin <https://github.com/OpenMediaVault-Plugin-Developers/openmediavault-openvpn>`_
	by omv-extras.

文件 :file:`/etc/openmediavault/config.xml` 是干什么用的？
	Is the database configuration store file for |omv|. When a change is
	performed in the |webui|, the config value is stored and/or retrieved by
	RPC to/from this file. If this is a save change, then mkconf passes the
	value to the service configuration file and reloads the daemon in case
	is necessary.

我是否可以升级到 Debian 测试/不稳定版本？或者使用 Ubuntu 作为底层系统？
	Yes. But the end is most likely a broken |webui| and possibly broken
	system. |omv| releases are heavily tight to their Debian base distribution.

忘记了 |webui| 密码。该如何重置？
	Simply connect via ssh into the server or login locally on the machine
	and type in: :command:`omv-firstaid`. There is an option to reset the
	|webui| password.

我是否可以备份或还原已存在的 |omv| 配置文件？
	No. Keep the file :file:`/etc/openmediavault/config.xml` for references
	purposes if the option is to go for a clean re-install.

|omv| 的默认 HTTP 引擎是什么？
	NGINX. The last version of |omv| with Apache was 0.5 Sardoukar.

是否可以改用 Apache 作为默认的 HTTP 引擎？
	Yes, but is not supported. Eventually every |omv| package upgrade will
	activate NGINX again leaving the |webui| broken. A parallel Apache
	instance next to Nginx is possible, just make sure the ports are different
	otherwise the |omv| |webui| will not work.

如何使用默认的 HTTP 引擎托管我自己的网站内容？
	Do not modify |omv| default NGINX files. Place the website configurations
	in :file:`/etc/nginx/sites-available` and enable it with
	:command:`nginx_ensite <SITE>`. Read more information in the
	`NGINX documentation <http://nginx.org/en/docs/>`_.

Why does the system rewrites a configuration file(s) that I have manually edited?
	OMV takes full control of some system services. This services include
	monit, ntp, samba, network, proftpd, nginx, php5-fpm, etc. Read
	:doc:`here </various/files>`.

How can I modify an internal value of some service |omv| has control over?
	Read :doc:`here <various/advset>` for advanced configurations.

How can I modify or add a network configuration of :file:`/etc/network/interfaces` with some custom options the |webui| does not provide?
	The interfaces file is controlled by |omv|. To add network interfaces
	that are not configurable through the |webui| or other options not present,
	use  :doc:`advanced settings <various/advset>`.

为什么磁盘的挂载路径是长长的一串字母？
	The long number is called UUID, it is used by fstab to mount disks. This
	number is unique per filesystem (or at least unlikely possible that
	another filesystem comes with an identical one). This helps maintaining the
	mount points. The old linux way (sda1, sdb1, etc.) is not guaranteed that
	/sda1 is the same disk on next reboot. If having trouble identifying them
	in terminal, create a pool with symlinks to each file system with easy to
	remember names.

	This behaviour has been deprecated now in current omv releases including
	stable (Jessie). The default creation of mount paths is documented
	`here <https://github.com/openmediavault/openmediavault/blob/20ec529737e6eca2e1f98d0b3d1ade16a3c338e1/deb/openmediavault/usr/share/openmediavault/engined/rpc/filesystemmgmt.inc#L823-L833>`_.

我没有数据盘，想把数据存储到系统盘上可以吗？
	|omv| 作为一个 NAS 服务器的首要行为就是将系统与数据分离开。

	However if the OS disk is partitioned the system will recognise the extra
	partitions besides rootfs if is formatted. You can mount it and use it for
	shared folders.

	The current installer does not provide access to the partition manager,
	use a plain Debian iso then install |omv| on top and acommodate the
	partitions, or resize the partition after installing using Gparted or
	SystemRescueCd.

|omv| 是否可以安装到现有的 Debian 系统中？
	是的，但建议现有的 Debian 系统不要安装桌面环境。

What is the permissions/ownership of folders in |omv| created by shared folders?
	The default is folders in ``2775`` mode, with ``root:users`` ownership.
	This means all users created in the |webui| can read, write to folders
	created by the system in the data drives using the default. The setgid allows
	group inheritance, meaning new files/folders below will always have the group
	users (GID=100) membership.

Why are my filesystems mounted as noexec?
	This is a security measure to avoid the placement of malicious scripts in
	the shared folders. This will prevent any script execution in those paths,
	including compiling packages and binaries.

	If you need to remove the noexc flag, use advanced settings as decribed
	:doc:`here </various/fs_env_vars>`.

我需要删除共享，为什么删除按钮是灰色/禁用的？
	Shared folder configurations can be used across different services. When
	removing a shared folder configuration is necessary to unlink it from
	every service is attached to, before the delete button becomes available.
	At the moment there is no internal database backend that can display
	information about which service is holding which shares.

:command:`omv-mkconf` 命令有什么用？
	:command:`omv-mkconf` is a terminal console command that is used by the
	backend of |omv| to pipe directives and values to service configuration
	files. The arguments that :command:`omv-mkconf` accepts are related to the
	name of the service it configures. Type :command:`omv-mkconf` in terminal,
	press TAB key, and the terminal will display all available arguments.

I want to experiment with |omv| or make changes to the code
	As a true open source system everything is possible. The
	recommendation is do not test with the production server to avoid
	breaking the |webui|. The best thing to do is to use a Virtual Machine.
	On `Sourceforge <http://sourceforge.net/projects/openmediavault/files/vm/VirtualBox%20images/>`_
	there are preconfigured |omv| images with virtual disks ready to launch.
	Alternatively checkout the |omv| `GIT repository <https://scm.openmediavault.org/>`_
	and use `Vagrant <https://www.vagrantup.com/>`_ to create a virtual
	machine.

|omv| 4 为什么没有 iSCSI target 插件？
	The iscsitarget software is divided in two parts. The `userland tools <https://packages.debian.org/source/jessie/iscsitarget>`_
	and the `kernel modules <https://packages.debian.org/jessie/iscsitarget-dkms>`_ both are provided by Debian repository system.
	Kernel modules come in the form of `DKMS <https://en.wikipedia.org/wiki/Dynamic_Kernel_Module_Support>`_. 
	The upstream software is maintained in `sourceforge <https://sourceforge.net/projects/iscsitarget/files/iscsitarget/>`_.
	Debian only provides packages up to Jessie, this is because the DKMS modules do not built in kernels higher than 4.x.
	The last commit upstream was in 2010, right now iscsitarget is abandoned software.

	It is possible to use iscsitarget plugin in |omv| 3 or lower versions by using kernels lower than 4.x.

	The intention is to migrate core underlaying software from iscsitarget to `LIO targetcli <http://linux-iscsi.org/wiki/Targetcli>`_  

:command:`omv-update` 和 :command:`omv-release-upgrade` 两个命令有什么用？
	Information about those commands are in the software :doc:`section </various/apt>`.
