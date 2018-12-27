# LinuxSwap
Linux中的swap技术研究


<pre>
Swap简介：

         物理内存就是计算机的实际内存大小，由RAM芯片组成，虚拟内存是虚拟出来的，使用磁盘
      代替内存。虚拟内存的出现，让机器内存不够的情况得到部分解决，当程序运行起来由操作系统
      做具体的虚拟内存到物理内存的替换和加载，这里的虚拟内存就是所谓的swap.
</pre>

<pre>
    当物理内存使用完或者达到一定比例之后，我们可以使用swap做临时的内存使用。当物理内存
    和swap都被使用完那么就会出错，out of memory。对于使用多大比例内存之后开始使用swap，
    在系统的配置文件中可以通过调整参数进行修改。
	cat  /proc/sys/vm/swappiness
	60

    该参数可以从0-100进行设置。0就是最大限度使用内存，尽量不使用swap；100就是积极使用
    swap。这个具体的通过系统的算法进行确定。

    物理内存我们是无法更改的，所以swap的大小设置将会影响应用能否正常运行。那么swap大小如
    何确定。根据centos官网介绍可以得出如下公式：M = Amount of RAM in GB, and S = Amount of swap in GB, then If M < 2, S = M *2 Else S = M + 2。而且其最小不应
    该小于32M(never less than 32 MB.)。

    swap分区的数量对性能也有很大的影响。因为swap毕竟还是以磁盘来伪装成内存，交换的操作是
    磁盘IO的操作而不是内存的load与store操作。如果有多个swap交换区，每个swap会有一定的优
    先级，该优先级也可以调整。swap空间的分配会以轮流的方式操作于所有的swap，这样会大大均
    衡IO的负载，加快swap交换的速度。
</pre>


