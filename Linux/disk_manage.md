# 磁盘管理

## Tips
### /sys/
/sys/block/sd\[abcde\]    link文件
```
root@929200:/sys/devices# ll /sys/block/sd*
lrwxrwxrwx 1 root root 0 Nov  2 20:04 /sys/block/sda -> ../devices/pci0000:00/0000:00:01.0/0000:01:00.0/host0/port-0:0/end_device-0:0/target0:0:0/0:0:0:0/block/sda/

lrwxrwxrwx 1 root root 0 Nov  4 23:52 /sys/block/sdb -> ../devices/ pci0000:80/ 0000:80:02.0/ 0000:81:00.0/ host2/ port-2:0/ expander-2:0/ port-2:0:5/ end_device-2:0:5/ target2:0:5/ 2:0:5:0/ block/ sdb/
lrwxrwxrwx 1 root root 0 Nov  4 23:54 /sys/block/sdc -> ../devices/ pci0000:80/ 0000:80:02.0/ 0000:81:00.0/ host2/ port-2:0/ expander-2:0/ port-2:0:6/ end_device-2:0:6/ target2:0:6/ 2:0:6:0/ block/ sdc/
lrwxrwxrwx 1 root root 0 Nov  4 23:54 /sys/block/sdd -> ../devices/ pci0000:80/ 0000:80:02.0/ 0000:81:00.0/ host2/ port-2:0/ expander-2:0/ port-2:0:7/ end_device-2:0:7/ target2:0:7/ 2:0:7:0/ block/ sdd/
lrwxrwxrwx 1 root root 0 Nov  4 23:54 /sys/block/sde -> ../devices/ pci0000:80/ 0000:80:02.0/ 0000:81:00.0/ host2/ port-2:0/ expander-2:0/ port-2:0:8/ end_device-2:0:8/ target2:0:8/ 2:0:8:0/ block/ sde/

lrwxrwxrwx 1 root root 0 Nov  4 23:55 /sys/block/sdf -> ../devices/ pci0000:00/ 0000:00:02.0/ 0000:02:00.0/ host1/ port-1:0/ expander-1:0/ port-1:0:5/ end_device-1:0:5/ target1:0:5/ 1:0:5:0/ block/ sdf/
lrwxrwxrwx 1 root root 0 Nov  4 23:55 /sys/block/sdg -> ../devices/ pci0000:00/ 0000:00:02.0/ 0000:02:00.0/ host1/ port-1:0/ expander-1:0/ port-1:0:6/ end_device-1:0:6/ target1:0:6/ 1:0:6:0/ block/ sdg/
lrwxrwxrwx 1 root root 0 Nov  4 23:56 /sys/block/sdh -> ../devices/ pci0000:00/ 0000:00:02.0/ 0000:02:00.0/ host1/ port-1:0/ expander-1:0/ port-1:0:7/ end_device-1:0:7/ target1:0:7/ 1:0:7:0/ block/ sdh/
lrwxrwxrwx 1 root root 0 Nov  5 00:07 /sys/block/sdi -> ../devices/ pci0000:00/ 0000:00:02.0/ 0000:02:00.0/ host1/ port-1:0/ expander-1:0/ port-1:0:8/ end_device-1:0:8/ target1:0:8/ 1:0:8:0/ block/ sdi/
```

总结一下，按照理想中的`/dev/sd*`与`磁盘`的对应情况：  
前四个磁盘的文件在`/dev/ devices/ pci0000:80/ 0000:80:02.0/ 0000:81:00.0/ host2/ port-2:0/ expander-2:0/ port-2:0:[5678]/ end_device-2:0:[5678]/ target2:0:[5678]/ 2:0:[5678]:0/ block/ sd[bcde]`  
后四个磁盘的文件在`/dev/ devices/ pci0000:00/ 0000:00:02.0/ 0000:02:00.0/ host1/ port-1:0/ expander-1:0/ port-1:0:[5678]/ end_device-1:0:[5678]/ target1:0:[5678]/ 1:0:[5678]:0/ block/ sd[fghi]`

````
echo 'offline' > /sys/block/sdb/device/state
echo '1' > /sys/block/sdb/device/delete   # 这条命令导致这个磁盘再也无法被识别到/dev/sdb
````

### fio

https://serverfault.com/questions/93783/make-a-hard-disk-sleep-and-only-wake-up-when-needed

## 常用命令

### 查看各种设备的命令
```
lscpu    # 用于查询CPU信息
lshw     # 用于显示硬件信息表
hwinfo   # 用于查询硬件信息
lsppci   # 用于列出PCI总线的信息以及连接到PCI总线上的设备信息
lsusb    # 用于列出USB总线信息
lsblk    # 用于列出块设备的信息
lsscsi   # 用于列出SCSI的设备信息
```
readlink sda

### fdisk

### gdisk
linux 创建文件系统 对`整个磁盘` OR 对`单一分区`


### mkfs
```
mkfs.exit4 /dev/sdb
mkfs -t ext4 /dev/sdb
```

### tune2fs
    tune2fs -l /dev/sdb

### mount umount
```
mount -t ext4 /dev/sdb  /media/hdd01
umount /dev/vdb
```

/etc/fstab



### eject
    eject -v /dev/sdb

### scsi-spin
    scsi-spin --force --down /dev/sdc

### udisks
```
udisks --detach /dev/sdb
udisks --show-info /dev/sdb
udisksctl
```



### hdparm
hdparm命令提供了一个命令行的接口用于读取和设置IDE或SCSI硬盘参数。
```
hdparm -S 60 /dev/sdb   # 将sdb置为 idle mode，并设置 60s 超时阈值
hdparm -y /dev/sdb   # 将sdb置为 standby mode
```

```
具体参数：
-B  Get/set Advanced Power Management feature.
    小值意味着激进的能耗管理，大值意味着更高的性能。
    1~127: 允许spin-down
    128~254: 不允许spin-down
    255: 取消APM

-C  Check the current IDE power mode status.
    查询磁盘当前状态，返回值为以下几种：
    unknown (drive does not support  this  command)
    active/idle (normal operation), 
    standby (low power mode, drive has spun down)
    sleeping (lowest power mode, drive is completely shut down)

-S  Put the drive into idle (low-power) mode, and also set the standby (spindown) timeout for the drive.
    将磁盘置于 idle mode，并设置 standby (spindown) timeout。
    0: 不设置阈值，不会自动进入 standby mode
    1~240: 阈值为 5x，即 5s~20min
    241~251: 阈值为 (x-240)*30min，即 30min~5.5h
    252: 21min
    253: 厂商自行设置，范围 8-12h
    254: 保留
    255: 21min plus 15s

-y  Force an IDE drive to immediately enter the low power consumption standby mode, 
    usually causing it to spin down.
    使磁盘立即进入 standby mode。


-Y  Force  an  IDE  drive to immediately enter the lowest power consumption sleep mode, 
    causing it to shut down completely.
    使磁盘立即进入 sleep mode。

-Z  关闭某些Seagate硬盘的自动省电功能。
```

### 磁盘盘符与卡位对应关系

开机时所有磁盘一起通电，以随机的顺序被系统识别，按被识别的顺序依次命名为 sdb, sdc, ...
可用 `dmesg | grep -i sata` 查询识别顺序，建立磁盘盘符与卡位对应关系。

一个可能的对应关系如下：
```
HDD0    sdg
HDD2    sdf
HDD4    sdh
HDD6    sdi
HDD8    sde
HDD10   sdd
HDD12   sdb
HDD14   sdc
```


