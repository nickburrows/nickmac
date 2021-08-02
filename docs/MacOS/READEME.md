---
---

# MacOS Automator

## 在 Finder 當前文件夾中建立新檔案

1. 開啟 `Automator`
2. 新增文件
3. 文件類型 `快速動作`
4. 右側 `工作流程接收`選項: **`沒有輸入項目`**
5. 新增動作 `執行AppleScript`
6. 將原代碼清除並將下列指令貼至文件中

   ```applescript
   on run {input, parameters}

    try

        tell application "Finder" to set the thisFolder to (folder of the front window) as alias

    on error -- if no folder is open in finder or focused in running application, set default location to desktop

        set the thisFolder to path to desktop folder

    end try

    set fileName to text returned of (display dialog "Create new .txt file named:" default answer "Untitled")
    set filePath to POSIX path of thisFolder
    set theFile to filePath & fileName
    set prefixString to "copy of "

    -- if filename already existing, this service will ask for a new filename
    tell application "Finder"

        repeat while exists file theFile as POSIX file

            set fileName to text returned of (display dialog "\"" & fileName & "\"  already exists, please provide another name:" default answer prefixString & "Untitled")
            set theFile to filePath & fileName
            set prefixString to prefixString & "copy of "
        end repeat

    end tell

    do shell script "touch \"" & theFile & "\""

    return input
   end run
   ```

7. 儲存檔案，並將文件命名為`CreateNewTextFile`
8. 切換至 Finder 視窗，Mac 上方工具列選擇 `Finder` > `服務` > `CreateNewTextFile`

Options:

- 可將此快速動作設置快捷鍵
  - `系統偏好設定` > `鍵盤` > `快速鍵` > `一般` > `CreateNewTextFile`
  - 加入欲新增的快速鍵組合
  - 即可於 Finder 視窗以快速鍵執行此動作
