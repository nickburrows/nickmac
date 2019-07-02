# MacOS 安裝 Aria2

## 安裝方式

- Step 1. 使用Homebrew安裝

```
brew search aria2
brew install aria2
```

- Step 2. 新增開機自動運行文件

在aria2安裝資料夾中新增文件"homebrew.mxcl.aria2.plist"，文件內容如下:

```plist
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

其中`--rpc-secret=TOKEN`的TOKEN設置需與`aria2.conf`中相同

- Step 3. 啟動aria2

```
brew services start aria2
```

## aria2相關配置

路徑`$HOME/.aria2./aria2.conf`

[配置文件參考](aria2.conf)
