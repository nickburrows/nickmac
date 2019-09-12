# Alfred安裝與配置說明

## Alfred 4啟動異常 解決方案

```bash
sudo codesign -f -s - --deep /Applications/Alfred\ 4.app
sudo codesign --sign - --force --deep /Applications/Alfred\ 4.app/Contents/Preferences/Alfred\ Preferences.app
```

### 指令參考

```bash
sudo codesign --force --deep --sign /Applications/APP_NAME.app
```

> macOS应用程序如果在打开时提示崩溃，该怎么解决？最近一次Apple静默更新之后，Apple删除了TNT的证书，因此应用程序将在7月12日之后崩溃。目前的解决方案是自己签名。
>
> 检测软件签名是否存在
>
> 1. 打开终端，输入【`sudo -s`】
> 2. 然后会提示你输入开机密码，你就把密码输入***，输入过程中不会显示密码，输入完成后按确认键enter***
> 3. ***然后再终端输入【xattr 】，再打开应用程序文件夹，把软件拖到终端，比如把Winclone拖***，终端就会显示【`xattr /Applications/Winclone.app`】，然后按确认
> 4. 接下来你就会看到`com.apple.quarantine`，这样的结果，有的软件拖***按确认后会显示`com.apple.FinderInfo`这样的结果。
> 5. 如果有这样的反馈，说明此软件的签名在，正常情况是不会崩溃的。如果崩溃了，那就得清除这个签名。
>    清除签名
> 6. 清除签名的命令`xattr -r -d com.apple.quarantine /Applications/APP_NAME.app` 输入完成后按确认即可。
>
> 資料來源: https://zhuanlan.zhihu.com/p/73684413

### 開啟允許外部連結下載app

```bash
sudo spctl --master-disable
```

## 終端機更改為: iTerm

>[參考網站](http://louiszhai.github.io/2018/05/31/alfred/#alfred-workflow)

Alfred設置面板**Appearance**

在 _Terminal_ 分類中**_Application_ 更改為 _Custom_**，並將以下這段代碼貼上即可。

```
on alfred_script(q)
    tell application "iTerm"
        set _length to count window
    if _length = 0 then
        create window with default profile
    end if
    set aa to (get miniaturized of current window)
    if aa then
        set miniaturized of current window to false
    end if
    set bb to (get visible of current window)
    if bb is false then
        set visible of current window to true
    end if
    set cc to frontmost
    if cc is false then
        activate
    end if
        (*if _length = 0 then*)
            set theResult to current tab of current window
        (*else
            set theResult to (create tab with default profile) of current window
        end if*)
        write session of theResult text q
end tell
end alfred_script
```

#### 此為Alfred預設原代碼：

```
on alfred_script(q)
	tell application "Terminal"
		activate
		do script q
	end tell
end alfred_script
```
