# MacOS 安裝 Aria2

## 安裝方式

- Step 1. 使用Homebrew安裝

```
brew search aria2
brew install aria2
```

- Step 2. 新增開機自動運行文件
  - 在aria2資料夾中新增開機自動運行文件"[homebrew.mxcl.aria2.plist](homebrew.mxcl.aria2.plist)"，
  - 如使用Homebrew方式安裝，參考路徑: `/usr/local/Cellar/aria2/[版本XXX]/`
  - `--rpc-secret=TOKEN`，**TOKEN**需與aria2.conf中[`rpc-secret=<TOKEN>`](aria2.conf#L68)中設置相同

範例:

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



- Step 3. 啟動aria2

```
brew services start aria2
```

### 配置文件 `aria2.conf`

參考路徑: `$HOME/.aria2./aria2.conf`，[配置範例](aria2.conf)
