# 概述
中国大陆车友使用Wahoo Fitness码表，因为不可描述的原因，（除了特定的条件下）无法通过互联网正常升级固件，许多车友不得不频繁至当地车店进行有偿或无偿服务才能顺利升级。故特开此项目。保存码表的官方升级包以及离线升级方法（非ADB），简单地复制文件即可完成升级。
当然由于Wahoo码表固件采用的是极致裁剪的Android架构，但还是Android，adb大法也是可行的，但是由于adb安装依赖工具链的门槛对于非码农来说实在太高，在此不做赘述。有兴趣的可以[ 到b站查看 ](https://www.bilibili.com/video/BV1YT4y1F7AW/)（非本文所述方法） 。

最新版本 2020-9-10 [13311](https://gitee.com/assofour/wahoouptCN/blob/main/firmware/BoltApp13311.apk) 
# 免责
以下内容均为器材爱好者的极端不负责任的自我尝试，如遇失败，无效变砖等等不可预期之后果，本人不承担任何道德以及法律责任。
WAHOO™, Elemnt Bolt, Elemnt Roam 均是Wahoo Fitness L.L.C.的注册商标。

# 适用范围
Wahoo目前发布的码表有Elemnt（停产）, Elemnt Bolt（停产）, Elemnt Roam, new Elemnt Bolt（或者称为 v2)，以下方法已经经过验证截止<b>July 2, 2021</b>可以成功升级的有:

- Elemnt Bolt（停产）
- Elemnt Roam
- new Elemnt Bolt（或者称为 v2)

以下Windows系统已验证的有

- Windows 10

以下Mac OS系统已验证的有

- Mac OS Big Sur 11.4

所有的固件均根据Wahoo[官方的版本检查文件](http://bolt.wahoofitness.com/boltapp/version.json)下载，无任何修改。如有能力，可以自行下载。 Std-version是正式版本（有时候官网还没有宣发，这里已经能看到更新的版本了），beta-version是测试版本，可以尝鲜，alpha这种版本不建议了。

2021年7月2日文件样本
```
{
  "std-version": 12072,
  "std-url": "https://wahoo-cloud-eu.wahooligan.com/firmware/elemnt/boltapp/12072/BoltApp.apk",
  "beta-version": 12072,
  "beta-url": "https://wahoo-cloud-eu.wahooligan.com/firmware/elemnt/boltapp/12072/BoltApp.apk",
  "alpha-version": 12504,
  "alpha-url": "https://wahoo-cloud-eu.wahooligan.com/firmware/elemnt/boltapp/12504/BoltApp.apk"
}
```

- [ ] Todo: Add a script to pull down files automatically.

# 简单固件文件升级方法（推荐）

## 获得固件升级文件

从项目仓库的文件列表中，[进入firmware目录](https://gitee.com/assofour/wahoouptCN/tree/main/firmware)，所有的固件都采用
BoltApp + 版本号 + .apk
的模式进行命名，最新的固件版本号一定是最高的那个，此处仅提供正式发布的标准版固件。找到文件后，下载至本地磁盘并按如下一节描述对文件进行改名处理。

## 文件命名
虽然从下载的域名以及文件名内使用了Bolt的字样，但是无论从版本号，还是实践来看这个版本里所指示的固件适用于“适用范围”里面已经验证的机型。原始文件命名是BoltApp.apk，但在复制到文件系统内时，必须去除“.apk”的后缀名。例如“BoltApp12072.apk”修改为"BoltApp"，注意大小写严格遵循这个式样。

## 连接电脑传输文件
### Windows 操作系统
一般来说，使用USB电缆在“开机”状态下连接码表和PC USB端口，无需驱动，能在文件管理器里直接访问码表的部分文件系统，找到“system update elemnt”目录，在此目录之下新建一个目录，命名方式为版本号，例如版本11604，那么新建目录严格为“11604”，并在该目录下，复制“BoltApp”文件放入。

### Mac OS 操作系统
安装Google官方的Android File Transfer应用，可从[Google官方下载](https://dl.google.com/dl/androidjumper/mtp/current/AndroidFileTransfer.dmg), 或从项目仓库[下载安装文件](https://gitee.com/assofour/wahoouptCN.git)。使用USB电缆在“开机”状态下连接码表和Mac的USB端口，无需驱动，Android File Transfer应用自动打开并列出可访问的文件系统，找到“system update elemnt”目录，在此目录之下新建一个目录，命名方式为版本号，例如版本11604，那么新建目录严格为“11604”，并在该目录下，复制“BoltApp”文件放入。

注意部分机型上会看到“system update”目录，<b>不要 不要 不要</b> 使用这个目录，轻则无效，重则变砖。

## 关机完成固件升级
以上文件传输完毕后，安全推出USB设备，拔除USB电缆，按下Power Off，按正常流程关机，如果一切顺利，可以看到下方出现“INSTALL...”字样说明已经在安装（可参见Bolt V2 Insting Sample.jpeg以及Elemnt Roam Insting Sample.jpeg），依据机型不同，通常在1-2分钟内完成后，自行重启。重启后，至SYSTEM INFO下查看版本号是否已经更新到预期。

# ADB固件文件升级方法（码农运用）
## 进入ADB Mode

Bolt V2进入ADB模式的方法很简单，开机后，断开USB电缆的情况下，连续快速按Power键两次后，重新连接USB电缆，在terminal运行。
以上方法在USB A - USB C上获得成功

```
adb devices
```
应输出

List of devices attached
43212xxxxxxx	device

如果是如下信息，那么就继续按按钮

List of devices attached
43212xxxxxx	unauthorized

## 运行升级命令

固件文件的获得参见以上节”获得固件升级文件“，注意本方法中，保留apk文件后缀名，在terminal中运行如下命令

```
adb install -r ./BoltApp.apk
```

之后界面直接出现 INSTALL... 字样，后自动重启，升级完成。如果以上都顺利完成了，让Bolt为你高歌一曲

```
adb shell am broadcast -a com.wahoofitness.bolt.service.BBuzzerManager.MARIO
```
# 彩蛋 - 地图升级

Wahoo的地图本身是采用了Openstreetmap（OSM）的底图数据，该数据可以在[OSM官网](https://www.openstreetmap.org/)下载。通过原始数据，通过[一个开源的脚本](https://github.com/treee111/wahooMapsCreator)进行数据处理和构建，可以获得在Wahoo码表上能使用的地图文件，地图缩放级别为8。然而，运行这个脚本需要先下载约9G原始底图，配置一堆本地OSM环境和工具以及数个小时的运行时间。如下谈及的地图是经过以上流程构建完成的地图文件，随取复制即可。简而言之，如果你更新不了地图，那么简单按照如下步骤执行，那么Wahoo上就有中国地图了。

地图的下载链接 更新于 2021-9-10

```
百度网盘 链接: https://pan.baidu.com/s/1mE_tE-XtbD4dg89naRHqoQ 提取码: jx6g
```

 - 下载地图到本地，通过某种工具解压缩，将看到各种一大堆的数字命名的目录
 - 将这些目录复制到 \maps\tiles\8\ 下，目录结构请见 Device Map Dir Structure.png
 - 删除\maps\temp\下所有的临时文件
 - 重新启动码表，到导航视图下，看看路网是否出现

# 疑问和问题

如果你在这个过程中遇到任何问题，请在Issues中提出，我尽可能回答和帮助。
