## macOS使用方法总结

### 键位

⌘——Command () win键

⌃ ——Control ctrl键

⌥——Option (alt)

⇧——Shift

⇪——Caps Lock

fn——功能键就是fn

### hidpi

https://github.com/xzhih/one-key-hidpi/blob/master/README-zh.md

1920x1080

1632x918

1440x810



### CSR

```
csrutil status
csrutil authenticated-root status
```

```
csrutil disable
csrutil authenticated-root disable
```



### 打开/关闭显示所有文件

```
defaults write com.apple.finder AppleShowAllFiles -boolean true;killall Finder
defaults write com.apple.finder AppleShowAllFiles -boolean false;killall Finder
```

| 版本号 | 名称        | 下载地址                                                     |
| ------ | ----------- | ------------------------------------------------------------ |
| 10.15  | Catalina    | https://apps.apple.com/jp/app/macos-catalina/id1466841314    |
| 10.14  | Mojave      | https://apps.apple.com/jp/app/macos-mojave/id1398502828      |
| 10.13  | High Sierra | https://apps.apple.com/jp/app/macos-high-sierra/id1246284741 |
| 10.12  | Sierra      | https://apps.apple.com/jp/app/macos-sierra/id1127487414      |
| 10.11  | El Capitan  | https://apps.apple.com/app/os-x-el-capitan/id1147835434      |



### 制作 macOS 启动介质   

```
sudo /Applications/Install\ macOS\ Catalina.app/Contents/Resources/createinstallmedia --volume /Volumes/Install\ macOS\ Catalina
```

 注意：需要将.app文件置于 Applications(应用程序) 文件夹下。



### 重置NVRAM

`option` + `command` + `P` + `R`



SMC重置：Mac关机后，按住电源键10秒

SMC重置 步骤2：右侧的Shift键、左侧的Option键和Control键 7 秒钟

PRAM/NVRAM 重置：Option，Command，P，R。



### NVRAM 测试

```
sudo nvram TestVar=HelloWorld;
sudo nvram -p | grep 'TestVar';
```

​        

### 软件索引

[Old Mac 软件](https://www.macintoshrepository.org/applications/?c=267&p=1)     

[mac-torrent-download](https://mac-torrent-download.net)

https://mac-torrent-download.net/?s=  

