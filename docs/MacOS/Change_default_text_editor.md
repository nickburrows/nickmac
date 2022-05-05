# MacOS 更改預設文字編輯器

本次最大功臣來自這篇 [絕世好文](https://apple.stackexchange.com/questions/123833/replace-text-edit-as-the-default-text-editor) ，不囉唆直接給五星好評！

## 前因

因為慣用的文字編輯器為 `Visual Studio Code` ，且在多數時候需要開啟的文件不一定都是 `text` 的純文字檔，但仍需以`VSCode`開啟使用，無論是透過文件資訊修改開啟的應用程式、拖曳至Dock以 `VSCode` 開啟、甚至用 `Automator` 建立一個快速操作的腳本...都仍然不能滿足我的需求（因為還有各種 `.xxxx` 的檔案類型都算是純文字檔），但隨著新的技術之類的這種原因而造成這類的純文字檔越來越多種，一個一個改、每次都要經過一番操作才能用習慣的編輯器來開啟實在太累了，於是再努力一番搜索之後總算找到一些方式來修改MacOS的預設文字編輯器了（對我來說簡直完美，所以要趕快記下來，終於可以跟MacOS的文字編輯器說Bye Bye~）

## 解決方式

- `Homebrew` 安裝 `duti`

```bash
❯ brew install duti
```

- 取得 `Visual Studio Code` 的應用程式辨識資訊，等下會使用到
- 更多關於 [CFBundleIdentifer](https://developer.apple.com/documentation/bundleresources/information_property_list/cfbundleidentifier) 的說明

```bash
❯ /usr/libexec/PlistBuddy -c 'Print CFBundleIdentifier' /Applications/Visual\ Studio\ Code.app/Contents/Info.plist
com.microsoft.VSCode
```

- 用 [`duti`](https://github.com/moretension/duti/) 和剛剛取得的 `com.microsoft.VSCode` 來替 `MacOS` 修改預設的應用程式
- 將VSCode設為 _檔案類型屬於 **文字**_ 的預設應用程式

```bash
❯ duti -s com.microsoft.VSCode public.plain-text all
```

- 沒有拓展名的檔案類型

```bash
❯ duti -s com.microsoft.VSCode public.unix-executable all
```

- 檔案類型屬於文字，但不是一般的 `text` 檔案

```bash
❯ duti -s com.microsoft.VSCode public.data all
```

如此一來就解決了每次要開啟 **文字類型的檔案** ，但又不是 `text` 的檔案時，就能用自己慣用的文字編輯器開啟了。覺得舒服多了
