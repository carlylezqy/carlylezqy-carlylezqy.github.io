### VMWare 将物理硬盘映射为 vmdk

```
diskutil list
/Applications/VMware\ Fusion.app/Contents/Library/vmware-rawdiskCreator  create /dev/disk4 fullDevice usb-hdd ide
```

```
ide1:0.present="TRUE"
ide1:0.fileName="usb-hdd.vmdk"
```

### **DSM**崩溃恢复方法
1. 复制全新虚拟机磁盘文件 [.vmdk] [-flat.vmdk] 到虚拟机内部
2. VMWare设置中移除数据盘。注意：虚拟机磁盘文件名必须与[-flat.vmdk]文件内部包含的文件名一致
3. 启动虚拟机并全新安装后添加数据盘

