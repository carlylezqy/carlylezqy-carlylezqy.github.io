**[**1] 黑苹果页面



开启任意来源

sudo spctl --master-disable



黑苹果软件 

https://mac-torrent-download.net

https://mac-torrent-download.net/?s=

http://www.hzcourse.com/web/refbook/probationAll/7873/cc47c9db234b49f8a6d0351f4a0c0bc8



显示隐藏所有文件

defaults write com.apple.finder AppleShowAllFiles -boolean true;killall Finder

defaults write com.apple.finder AppleShowAllFiles -boolean false;killall Finder

| 10.15 | [Catalina](https://apps.apple.com/jp/app/macos-catalina/id1466841314) | https://apps.apple.com/jp/app/macos-catalina/id1466841314    |
| ----- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 10.14 | [Mojave](https://apps.apple.com/jp/app/macos-mojave/id1398502828) | https://apps.apple.com/jp/app/macos-mojave/id1398502828      |
| 10.13 | [High Sierra](https://apps.apple.com/jp/app/macos-high-sierra/id1246284741) | https://apps.apple.com/jp/app/macos-high-sierra/id1246284741 |
| 10.12 | [Sierra](https://apps.apple.com/jp/app/macos-high-sierra/id1246284741) | https://apps.apple.com/jp/app/macos-high-sierra/id1246284741 |
| 10.11 | [El Capitan](https://apps.apple.com/app/os-x-el-capitan/id1147835434) | https://apps.apple.com/app/os-x-el-capitan/id1147835434      |

sudo /Applications/Install\ macOS\ [Catalina](https://apps.apple.com/jp/app/macos-mojave/id1398502828).app/Contents/Resources/createinstallmedia --volume /Volumes/AppleInstall

sudo /TimeMachine/Install\ macOS\ Catalina.app/Contents/Resources/createinstallmedia --volume /Volumes/Install\ macOS\ Catalina



测试NVRAM

https://www.tonymacx86.com/threads/native-nvram-available.192920/

```
sudo nvram TestVar=HelloWorld;
sudo nvram -p | grep 'TestVar';
```



