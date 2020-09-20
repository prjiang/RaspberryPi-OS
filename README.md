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

連線後即可從電腦查看 Raspberry Pi 的 IP。

若之後想更改連線，可登入ssh 修改 wpa_supplicant.conf ，新增WiFi之帳號密碼。
```
pi@raspberrypi:~$ sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
```
> 參考資料: [基礎-命令列設置無線網路](https://www.raspberrypi.com.tw/2152/setting-up-wifi-with-the-command-line/)

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
成功登入ssh後，啟用 VNC Viewer。
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
