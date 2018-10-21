硬件配置要求
=============

安装 |omv| 前请先确认你的硬件是否支持。

* **CPU 处理器**: 任何 x86_64 或 ARM 架构处理器
* **RAM 内存**: 1 GiB 以上
* **HDD 硬盘**:

  * **系统盘**: 不低于 4 GiB
  * **数据盘**: 无限制

.. note::
   
   整个磁盘都会被用于系统和交换分区 [1]_，因此容量并不十分关键。|omv| 不支持数据存储在
   系统盘。

机械硬盘、SSD [2]_、DOM [3]_、CF [4]_ 或 USB 可移动磁盘 [5]_ 都可以用作系统盘。

如果使用 U 盘、移动硬盘等闪存，请注意是否支持静态负载平衡 (static wear leveling) [6]_，
没有这项技术的闪存可能用不多久就会损坏。同时建议安装和启用
:ref:`Flash Memory plugin <plugin_3rd_party>` 插件。系统盘完全被用于系统运行，
无法用于存储用户数据。


.. [1] https://en.wikipedia.org/wiki/Paging
.. [2] https://en.wikipedia.org/wiki/Solid-state_drive
.. [3] https://en.wikipedia.org/wiki/Solid-state_drive#DOM
.. [4] https://en.wikipedia.org/wiki/CompactFlash
.. [5] https://en.wikipedia.org/wiki/USB_flash_drive
.. [6] https://en.wikipedia.org/wiki/Wear_leveling
