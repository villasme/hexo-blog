---
title: linux
date: 2018-09-13 13:08:33
categories:
- linux
tags:
- linux
- archLinux
- unbuntu命令及问题
---

## ubuntun挂载widnow-ntfs格式的分区

```bash
mkdir ~/windows/
sudo mount -t ntfs-3g -o remove_hiberfile /dev/nvme0n1p4 ~/windows/
```

## unbuntu下 service添加删除

```bash
Ubuntu也提供了另外一个简单的命令来实现管理。但首先服务必须已在/etc/init.d目录中存在。如：

添加一个服务: sudo update-rc.d ServiceName defaults

删除一个服务: sudo update-rc.d ServiceName remove

还可以安装另外一个比较强的工具: sudo apt-get install sysv-rc-conf sysvconfig

启动: sudo sysv-rc-conf 它可心配置各服务在各级别上的启动情况.

随时想启动某个服务, 可以这样: sudo /etc/init.d/ServiceName start
```
--------------------------
参考链接：
* [service 添加删除](https://blog.csdn.net/yuanchao99/article/details/9111269)


# archLinux 安装

- [archLiunx 以官网wiki的方式安装archLiuxn](https://www.viseator.com/2017/05/17/arch_install/)
- [archLinux 安装包](http://mirrors.163.com/archlinux/iso/2018.08.01/)
- [archLinux 必须配置 与 安装图形界面](https://www.viseator.com/2017/05/19/arch_setup/)
- [棒@简书安装 archLinux 教程](https://www.jianshu.com/p/3d3da6b930a1)
- [下载Arch引导镜像](https://www.archlinux.org/download/)
- [mac 下制作linux 优盘启动](https://my.oschina.net/u/2306127/blog/478288)
- [vscode 安装](https://www.jianshu.com/p/b2c3019fedcb)
- [chorme vscode 安装 这是个博客地址](http://caosiyang.github.io/2018/02/20/manjaro/)
- [yaourt 安装](https://blog.csdn.net/gddxz_zhouhao/article/details/53466977)
    * 这样解决的 最后 上面的 没有用
    ``` bash
        [archlinuxfr]
        Server = http://repo-fr.archlinuxcn.org/$arch
    ```

## 出现的问题

[airootfs 错误原来地址](http://www.kbase101.com/question/28839.html)
```
好像你应该在chroot中grub2-mkconfig 而不是在外面做它。 grub2-mkconfig使用grub-probe来检测与挂载点关联的真实设备，而airootfs（archiso的rootfs）被加载到ram中并且没有规范路径。

所以在安装grub和生成配置之前，先执行此操作：

arch-chroot /mnt /bin/bash  （可以执行现在与 grub-install）
```