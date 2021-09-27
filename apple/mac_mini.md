**[**2] Mac Mini



Old Mac 软件

https://www.macintoshrepository.org/applications/?c=267&p=1



VMWare 映射物理硬盘

diskutil list

/Applications/VMware\ Fusion.app/Contents/Library/vmware-rawdiskCreator create /dev/disk4 fullDevice usb-hdd ide



ide1:0.present="TRUE"

ide1:0.fileName="usb-hdd.vmdk"



MacPro 23位EFI

https://github.com/Piker-Alpha/macosxbootloader



sudo chflags nouchg （ここにboot.efiファイルをドラッグ） #ロックを外す

sudo chflags uchg （ここにboot.efiファイルをドラッグ） #ロックをかける



CSR相关

csrutil disable



显示隐藏文件

defaults write com.apple.finder AppleShowAllFiles -boolean true

defaults delete com.apple.finder AppleShowAllFiles

killall Finder



System\Library\CoreServices

usr\standalone\i386



修改受支持的机型

vi /Volumes/Mac OS X Install ESD/System/Library/CoreServices/PlatformSupport.plist





http://www.xlr8yourmac.com/systems/mac_mini_core_2_duo_swaps.html

https://post.m.smzdm.com/p/akmrk078/

https://bbs.feng.com/read-htm-tid-6879759.html



sudo /Contents/Resources/createinstallmedia --volume 

createinstallmedia --volume /Volumes/a --applicationpath ""

sudo /Contents/Resources/createinstallmedia --volume /Volumes/*a*



https://www.tonymacx86.com/threads/guide-lenovo-thinkpad-x240.245583/



img 转换 vmdk

/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

brew install qemu

qemu-img convert -f raw /Volumes/Data/synoboot.img -O vmdk /Volumes/Data/synoboot_

**DS3615xs**.vmdk



映射物理硬盘

此外很多用户使用NAS会有一个使用场景，就是让NAS分出来一定空间来给电脑使用，对于笔电这样硬盘较小的设备时这个功能就尤为实用。如果需要ISCSI功能的话在存储与快照总管中设置好你需要的**ISCSI**空间即可。之后在电脑端实用**ISCSI**发起程序中查看并连接对应的ISCSI。

![](https://raw.githubusercontent.com/carlylezqy/PictureBed/main/note_img/iSCSI%E5%8F%91%E8%B5%B7%E7%A8%8B%E5%BA%8F)

之后在电脑管理中找到磁盘管理，就可以看到一个需要初始化的磁盘，选择磁盘模式一路下一步就可以使用了。