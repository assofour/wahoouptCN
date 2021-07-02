# 概述
中国大陆车友使用Wahoo Fitness码表，因为不可描述的原因，（除了特定的条件下）无法通过互联网正常升级固件，许多车友不得不频繁至当地车店进行有偿或无偿服务才能顺利升级。故特开此项目。保存码表的官方升级包以及离线升级方法（非ADB），简单地复制文件即可完成升级。
当然由于Wahoo码表固件采用的是极致裁剪的Android架构，但还是Android，adb大法也是可行的，但是由于adb安装依赖工具链的门槛对于非码农来说实在太高，在此不做赘述。有兴趣的可以到b站查看 https://www.bilibili.com/video/BV1YT4y1F7AW/。

# 免责
以下内容均为器材爱好者的极端不负责任的自我尝试，如遇失败，无效变砖等等不可预期之后果，本人不承担任何道德以及法律责任。

# 适用范围
Wahoo目前发布的码表有Elemnt（停产）, Elemnt Bolt（停产）, Elemnt Roam, new Elemnt Bolt（或者称为 v2)，以下方法已经经过验证截止<b>July 2, 2021</b>可以成功升级的有:

- Elemnt Bolt（停产）
- Elemnt Roam
- new Elemnt Bolt（或者称为 v2)

以下Windows系统已验证的有

- Windows 10

以下Mac OS系统已验证的有

- Mac OS Big Sur 11.4

## 升级文件

### 获得文件

Wahoo官方的版本检查文件在 http://bolt.wahoofitness.com/boltapp/version.json 如有能力，可以自行下载。 Std-version是正式版本（有时候官网还没有宣发，这里已经能看到更新的版本了），beta-version是测试版本，可以尝鲜，alpha这种版本不建议了。

2021年7月2日文件样本
```git
{
  "std-version": 12072,
  "std-url": "https://wahoo-cloud-eu.wahooligan.com/firmware/elemnt/boltapp/12072/BoltApp.apk",
  "beta-version": 12072,
  "beta-url": "https://wahoo-cloud-eu.wahooligan.com/firmware/elemnt/boltapp/12072/BoltApp.apk",
  "alpha-version": 12504,
  "alpha-url": "https://wahoo-cloud-eu.wahooligan.com/firmware/elemnt/boltapp/12504/BoltApp.apk"
}
```

或从repo的列表中，进入firmware目录，所有的固件都采用
BoltApp + 版本号 + .apk
的模式进行命名，最新的固件版本号一定是最高的那个，此处仅提供正式发布的标准版固件。找到文件后，下载至本地磁盘并按如下一节描述对文件进行改名处理。
- [ ] Todo: Add a script to pull down files automatically.

### 文件命名
虽然从下载的域名以及文件名内使用了Bolt的字样，但是无论从版本号，还是实践来看这个版本里所指示的固件适用于“适用范围”里面已经验证的机型。原始文件命名是BoltApp.apk，但在复制到文件系统内时，必须去除“.apk”的后缀名。例如“BoltApp12072.apk”修改为"BoltApp"，注意大小写严格遵循这个式样。

## 连接电脑传输文件
### 连接电脑 Windows
一般来说，使用USB电缆在“开机”状态下连接码表和PC USB端口，无需驱动，能在文件管理器里直接访问码表的部分文件系统，找到“system update elemnt”目录，在此目录之下新建一个目录，命名方式为版本号，例如版本11604，那么新建目录严格为“11604”，并在该目录下，复制“BoltApp”文件放入。

### 连接电脑 Mac OS
安装Google官方的Android File Transfer应用，地址 https://dl.google.com/dl/androidjumper/mtp/current/AndroidFileTransfer.dmg, 或从repo下载。使用USB电缆在“开机”状态下连接码表和Mac的USB端口，无需驱动，Android File Transfer应用自动打开并列出可访问的文件系统，找到“system update elemnt”目录，在此目录之下新建一个目录，命名方式为版本号，例如版本11604，那么新建目录严格为“11604”，并在该目录下，复制“BoltApp”文件放入。

注意部分机型上会看到“system update”目录，<b>不要 不要 不要</b> 使用这个目录，轻则无效，重则变砖。

## 关机升级
以上文件传输完毕后，安全推出USB设备，拔除USB电缆，按下Power Off，按正常流程关机，如果一切顺利，可以看到下方出现“INSTALL...”字样说明已经在安装（可参见Bolt V2 Insting Sample.jpeg以及Elemnt Roam Insting Sample.jpeg），依据机型不同，通常在1-2分钟内完成后，自行重启。重启后，至SYSTEM INFO下查看版本号是否已经更新到预期。

DISCLAIMER

WAHOO™ 是Wahoo Fitness L.L.C.的注册商标。