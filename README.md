# How to create ISO for ubuntu

安装 systemback

```
sudo apt install systemback
sudo systemback
```

选择Live system create

勾选左侧的 include the user data files，这样自己主文件夹内的文件都会被包含在系统镜像中。要保证 /home有足够的空间

点击Create New按钮就开始创建了，等待创建完成

此时/home文件夹下会出现systemback_live_yyyy_mm_dd.sblive文件

若sblive文件小于4GB，可直接于systemback中选中你要转换的备份，点击convert to ISO导出ISO

若sblive文件大于4GB，需要：

使用deb包安装cdtools，之后

解压  .sblive 文件

```
mkdir sblive
tar -xf /home/systemback_live_2016-04-27.sblive -C sblive
```

重命名  syslinux 至 isolinux

```
mv sblive/syslinux/syslinux.cfg sblive/syslinux/isolinux.cfg
mv sblive/syslinux sblive/isolinux
```

解除ISO最大上限参数后导出ISO文件

```
mkisofs -iso-level 3 -r -V sblive -cache-inodes -J -l -b isolinux/isolinux.bin -no-emul-boot -boot-load-size 4 -boot-info-table -c isolinux/boot.cat -o sblive.iso -allow-limited-size sblive
```

完成后于用户目录可以找到对应的ISO镜像