# wahoouptCN
中国用户使用Wahoo码表，因为GFW的关系，无法通过互联网正常升级，在此保存码表的官方升级包以及离线升级方法（非ADB），简单地复制文件即可。

# 适用范围
Wahoo目前发布的码表有Elemnt, Elemnt Bolt, Elemnt Roam, new Elemnt Bolt（或者称为 v2)，以下方法已经经过验证截止July 2, 2021可以成功升级的有

-Elemnt Bolt
-<li>Elemnt Roam</li>
-<li>new Elemnt Bolt（或者称为 v2)</li>

以下Windows系统已验证的有

-<li>Windows 10</li>

以下Mac OS系统已验证的有

-<li>Mac OS Big Sur 11.4</li>

## 升级文件
### 命名
Wahoo官方的版本检查文件在 http://bolt.wahoofitness.com/boltapp/version.json ，虽然域名等适用Bolt的式样，但是无论从版本号，还是实践来看这个版本里所指示的固件适用于“适用范围”里面已经验证的机型。原始文件命名是BoltApp.apk，但在复制到文件系统内时，必须去除“.apk”的后缀名。

### 连接电脑 Windows
一般来说，使用USB电缆在“开机”状态下连接码表和PC USB端口，无需驱动，能在文件管理器里直接访问码表的部分文件系统，找到“system update elemnt”目录，在此目录之下新建一个目录，命名方式为版本号，例如版本11604，那么新建目录严格为“11604”，并在该目录下，复制“BoltApp”文件放入。

### 连接电脑 Mac OS
安装Google官方的Android File Transfer应用，地址https://dl.google.com/dl/androidjumper/mtp/current/AndroidFileTransfer.dmg, 或从repo下载。使用USB电缆在“开机”状态下连接码表和Mac的USB端口，无需驱动，Android File Transfer应用自动打开并列出可访问的文件系统，找到“system update elemnt”目录，在此目录之下新建一个目录，命名方式为版本号，例如版本11604，那么新建目录严格为“11604”，并在该目录下，复制“BoltApp”文件放入。

注意部分机型上会看到“system update”目录，<b>不要 不要 不要</b>使用这个目录，轻则无效，重则变砖。
