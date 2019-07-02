---
layout: page
title: 安裝Aria2
---

## 安裝方式

- Step 1. 使用**Homebrew**安裝

```
brew search aria2
brew install aria2
```

- Step 2. 新增開機自動運行文件
  - 在aria2資料夾中新增開機自動運行文件"[homebrew.mxcl.aria2.plist](homebrew.mxcl.aria2.plist)"，
  - 如使用Homebrew方式安裝，參考路徑: `/usr/local/Cellar/aria2/[版本XXX]/`
  - `--rpc-secret=TOKEN`，**TOKEN**需與aria2.conf中[`rpc-secret=<TOKEN>`](aria2.conf#L68)中設置相同


### `homebrew.mxcl.aria2.plist`

<details>
<summary>範例</summary>

```
<!--?xml version="1.0" encoding="UTF-8"?-->
<plist version="1.0">
    <dict>
<key>Label</key>
<string>homebrew.mxcl.aria2</string>
<key>ProgramArguments</key>
<array>
<string>/usr/local/opt/aria2/bin/aria2c</string>
<string>--enable-rpc=true</string>
<string>--rpc-secret=TOKEN</string>
<string>--rpc-allow-origin-all=true</string>
<string>--rpc-listen-all=true</string>
</array>
<key>RunAtLoad</key>
<true/>
<key>KeepAlive</key>
<true/>
</dict>
</plist>
```

</details>

- Step 3. 啟動aria2

```
brew services start aria2
```

### 配置文件 `aria2.conf`

參考路徑: `$HOME/.aria2./aria2.conf`，[aria2.conf文檔](aria2.conf)

#### `aria2.conf`

<details>
<summary>範例</summary>

```
## '#'開頭爲註釋內容, 選項都有相應的註釋說明, 根據需要修改 ##
## 被註釋的選項填寫的是默認值, 建議在需要修改時再取消註釋  ##

## 文件保存相關 ##

# 文件的保存路徑(可使用絕對路徑或相對路徑), 默認: 當前啓動位置
dir=/Users/nick/Documents/Backup_Exclude/Aria2
# 啓用磁盤緩存, 0爲禁用緩存, 需1.16以上版本, 默認:16M
#disk-cache=32M
# 文件預分配方式, 能有效降低磁盤碎片, 默認:prealloc
# 預分配所需時間: none < falloc ? trunc < prealloc
# falloc和trunc則需要文件系統和內核支持
# NTFS建議使用falloc, EXT3/4建議trunc, MAC 下需要註釋此項
#file-allocation=none
# 斷點續傳
continue=true

## 下載連接相關 ##

# 最大同時下載任務數, 運行時可修改, 默認:5
max-concurrent-downloads=5
# 同一服務器連接數, 添加時可指定, 默認:1
max-connection-per-server=16
# 最小文件分片大小, 添加時可指定, 取值範圍1M -1024M, 默認:20M
# 假定size=10M, 文件爲20MiB 則使用兩個來源下載; 文件爲15MiB 則使用一個來源下載
min-split-size=10M
# 單個任務最大線程數, 添加時可指定, 默認:5
split=32
# 整體下載速度限制, 運行時可修改, 默認:0
#max-overall-download-limit=0
# 單個任務下載速度限制, 默認:0
#max-download-limit=0
# 整體上傳速度限制, 運行時可修改, 默認:0
#max-overall-upload-limit=0
# 單個任務上傳速度限制, 默認:0
#max-upload-limit=0
# 禁用IPv6, 默認:false
#disable-ipv6=true
# 連接超時時間, 默認:60
#timeout=60
# 最大重試次數, 設置爲0表示不限制重試次數, 默認:5
#max-tries=5
# 設置重試等待的秒數, 默認:0
#retry-wait=0

## 進度保存相關 ##

# 從會話文件中讀取下載任務
input-file=/etc/aria2/aria2.session
# 在Aria2退出時保存`錯誤/未完成`的下載任務到會話文件
save-session=/etc/aria2/aria2.session
# 定時保存會話, 0爲退出時才保存, 需1.16.1以上版本, 默認:0
save-session-interval=60

## RPC相關設置 ##

# 啓用RPC, 默認:false
enable-rpc=true
# 允許所有來源, 默認:false
rpc-allow-origin-all=true
# 允許非外部訪問, 默認:false
rpc-listen-all=true
# 事件輪詢方式, 取值:[epoll, kqueue, port, poll, select], 不同系統默認值不同
#event-poll=select
# RPC監聽端口, 端口被佔用時可以修改, 默認:6800
#rpc-listen-port=6800
# 設置的RPC授權令牌, v1.18.4新增功能, 取代 --rpc-user 和 --rpc-passwd 選項
#rpc-secret=<TOKEN>
# 設置的RPC訪問用戶名, 此選項新版已廢棄, 建議改用 --rpc-secret 選項
#rpc-user=<USER>
# 設置的RPC訪問密碼, 此選項新版已廢棄, 建議改用 --rpc-secret 選項
#rpc-passwd=<PASSWD>
# 是否啓用 RPC 服務的 SSL/TLS 加密,
# 啓用加密後 RPC 服務需要使用 https 或者 wss 協議連接
#rpc-secure=true
# 在 RPC 服務中啓用 SSL/TLS 加密時的證書文件,
# 使用 PEM 格式時，您必須通過 --rpc-private-key 指定私鑰
#rpc-certificate=/path/to/certificate.pem
# 在 RPC 服務中啓用 SSL/TLS 加密時的私鑰文件
#rpc-private-key=/path/to/certificate.key

## BT/PT下載相關 ##

# 當下載的是一個種子(以.torrent結尾)時, 自動開始BT任務, 默認:true
#follow-torrent=true
# BT監聽端口, 當端口被屏蔽時使用, 默認:6881-6999
listen-port=51413
# 單個種子最大連接數, 默認:55
#bt-max-peers=55
# 打開DHT功能, PT需要禁用, 默認:true
enable-dht=false
# 打開IPv6 DHT功能, PT需要禁用
#enable-dht6=false
# DHT網絡監聽端口, 默認:6881-6999
#dht-listen-port=6881-6999
# 本地節點查找, PT需要禁用, 默認:false
#bt-enable-lpd=false
# 種子交換, PT需要禁用, 默認:true
enable-peer-exchange=false
# 每個種子限速, 對少種的PT很有用, 默認:50K
#bt-request-peer-speed-limit=50K
# 客戶端僞裝, PT需要
peer-id-prefix=-TR2770-
user-agent=Transmission/2.77
# 當種子的分享率達到這個數時, 自動停止做種, 0爲一直做種, 默認:1.0
seed-ratio=0
# 強制保存會話, 即使任務已經完成, 默認:false
# 較新的版本開啓後會在任務完成後依然保留.aria2文件
#force-save=false
# BT校驗相關, 默認:true
#bt-hash-check-seed=true
# 繼續之前的BT任務時, 無需再次校驗, 默認:false
bt-seed-unverified=true
# 保存磁力鏈接元數據爲種子文件(.torrent文件), 默認:false
bt-save-metadata=true

## MacOS 運行命令
# aria2c --conf-path="/Users/nick/.aria2/aria2.conf" -D

### 參考來源 ###
### https://www.twblogs.net/a/5b8cf86d2b7177188337e200
```

</details>
