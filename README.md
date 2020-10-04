# RaspberryPi4B-OS

## Step 1
### 作業系統
下載 [Raspberry Pi Imager](https://www.raspberrypi.org/downloads/) <b>(建議)</b> 或 [Raspberry Pi OS (previously called Raspbian)](https://www.raspberrypi.org/downloads/raspberry-pi-os/)，下載官方版較不會出現不相容問題。

將作業系統安裝至micro SD卡。
> 建議先將SD卡格式化。

<br>

新增空的ssh檔案(無副檔名) 及 製作WiFi設定檔。
> 參考資料: [樹莓派 Raspberry Pi，無頭式(無螢幕、鍵盤與滑鼠)，安裝到進入作業系統桌面~完整教學](https://home.gamer.com.tw/creationDetail.php?sn=3908401)

> 建議可以對電腦熱點進行連線，方便查找Raspberry Pi 的 IP 。

將 ssh 及 wpa_supplicant.conf 設定好放置boot。

完成後，將SD卡插入 Raspberry Pi 。

<br>

## Step 2
### SSH 登入
#### 抓取Raspberry Pi 的 IP
##### 方法一
將 Raspberry Pi 開啟，進入WiFi路由器的設定頁面，<b>抓取 Raspberry Pi 的 IP</b>。

##### 方法二
電腦開啟熱點，提供 Raspberry Pi 連線。

連線後即可從電腦的<b>熱點設定頁面</b>查看 Raspberry Pi 的 IP。

<br>

#### 登入 SSH
找出IP後，開啟 Windows PowerShell(系統管理員)，並登入ssh。
```
PS C:\WINDOWS\system32> ssh pi@Raspberry Pi 的IP
```
預設帳號為: <b>pi</b>

預設密碼為: <b>raspberry</b>

<br>

### 啟用 VNC 服務
成功登入ssh後，下載 [VNC Viewer](https://www.realvnc.com/en/connect/download/viewer/)。

開啟 VNC 。
```
pi@raspberrypi:~ $ sudo raspi-config
```
> Interfacing Options -> VNC -> Yes

重啟後，開啟 VNC Viewer 會出現錯誤!

<br>

### 錯誤解決
更改解析度即可解決，<b>不要選default</b>。
```
pi@raspberrypi:~ $ sudo raspi-config
```
> Advanced Options----Resolution----DMT85<b>（不要選default）</b>

<br>

完成後，重新啟動。
```
pi@raspberrypi:~ $ sudo reboot
```

<br>

VNC 登入後，即可見到 Raspberry Pi 系統。
> 參考資料: [樹莓派 raspberry 4B系統 VNC View 連接 Cannot currently show the desktop 錯誤解決](https://www.twblogs.net/a/5d4b3b75bd9eee5327fc11e1)

<br>

## Others
### 備份 SD 卡
下載[Win32 Disk Imager](https://sourceforge.net/projects/win32diskimager/)。

<b>裝置</b>選擇 Micro SD 卡位置，<b>映像檔</b>為存放位置，副檔名為img!

點選<b>讀取</b>

讀取成功後，即可退出 Micro SD 卡。
> 參考資料: [Raspberry Pi Win32 Disk Imager 備份 SD 卡教學](https://oranwind.org/-raspberry-pi-win32-disk-imager-bei-fen-sd-qia-jiao-xue/)

<br>

### 更改 Raspberry Pi 的預設網路連線
若想更改預設網路連線，可登入ssh 修改 wpa_supplicant.conf ，新增WiFi之帳號密碼。
```
pi@raspberrypi:~ $ sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
```
> 參考資料: [基礎-命令列設置無線網路](https://www.raspberrypi.com.tw/2152/setting-up-wifi-with-the-command-line/)

<br>

### 查看 Raspberry Pi 的 CPU 溫度
```
pi@raspberrypi:~ $ /opt/vc/bin/vcgencmd measure_temp
```

<br>

### 啟動後，Line Notify 發送啟動通知提醒

Line Notify 程式碼
```
#!/usr/bin/python
#-*-coding:utf-8-*-

import lineTool
import time
import datetime

Token = "填入你的Token"
TurnOn_message = "\n💡 Raspberry Pi 已啟動!\n"
Time_message = time.strftime("🕒 %Y-%m-%d %H:%M:%S", time.localtime())
MESSAGE = ''


time.sleep(10)
MESSAGE = TurnOn_message+ Time_message
print("Send message to Line \n%s\n" % MESSAGE)

lineTool.lineNotify(Token, MESSAGE)

input()
```
存檔後，設定 Corntab 每次 Raspberry Pi 啟動時運行命令。
```
crontab -e
```
所有＃開頭的都是註解，在文件最後加入以下命令。
```
@reboot python /home/pi/myscript.py
```
> 參考資料: [如何幫樹莓派安裝常用的Python套件(How to Install Python Package on Raspberry Pi)](https://www.slideshare.net/YanweiLiu1/pythonhow-to-install-python-package-on-raspberry-pi)

> 參考資料: [一起學 Python 107 : 五分鐘學會使用 Python 傳送 Line 訊息 在 Raspberry pi 開機啟動提醒](http://wyj-learning.blogspot.com/2018/07/python-106-python-line-raspberry-pi.html?m=1)

> 參考資料: [使用Cron安排任務](https://www.raspberrypi.org/documentation/linux/usage/cron.md)

<br>

### SyntaxError: Non-ASCII character ‘\xe4’ in file.
在程式碼開頭加入以下聲明字符格式。
```
#!/usr/bin/python
#-*-coding:utf-8-*-
```
