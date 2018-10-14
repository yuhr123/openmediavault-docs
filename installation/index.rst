.. _installation_index:

安装
############

开始之前：
	- 检查你的硬件是否满足 :doc:`硬件配置要求 </prerequisites>`。
	- `点此下载安装镜像 <https://sourceforge.net/projects/openmediavault/files/>`_，x86 架构请下载 ISO 镜像，ARM 架构请按型号选择预配置镜像。
	- 为了避免系统被不小心安装到数据盘上，建议除系统盘以外，断开所有其他硬盘。

安装方式：
	按照下列描述选择一种安装方式。

	* :doc:`安装系统到硬盘 </installation/via_iso>` - 建议通过 ISO 镜像安装，这样可以让 OMV 运行在独立的磁盘上。
	* :doc:`安装系统到 U 盘 </installation/on_usb>` - 这种方式在 U 盘上运行 |omv|。
	* :doc:`在 Debian 系统上安装 </installation/on_debian>` - 这种方式以服务的方式在 Debian 系统上运行 |omv|。
	* `在 Debian 系统上通过 deboostrap 安装 <https://forum.openmediavault.org/index.php/Thread/12070-GUIDE-DEBOOTSTRAP-Installing-Debian-into-a-folder-in-a-running-system/>`_ - 当系统无法识别 (NVME) 硬盘或某些网卡等需要更高版本内核 (backport) 支持的特殊硬件时，可以参考这种安装方案。
	* :doc:`安装到 SD 卡 </installation/via_image>` - 这种方式在 SD 卡上运行 |omv|。

初次使用：
	如果有显示器、KVM 或 IMPI 控制台，在登录界面上就能看到网页管理界面的 IP 地址。
	在浏览器中输入该 IP 地址即可打开登录界面，默认用户名和密码为
	``admin:openmediavault``，``root`` 密码则是你在安装时设置的。

  ARM 镜像的默认 ``root`` 密码为 ``openmediavault``。
