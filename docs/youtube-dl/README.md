---
youtube-dl
---

# 安裝 **youtube-dl**, **ffmpeg**

開啟終端機輸入指令 `brew install youtube-dl ffmpeg` 安裝youtube-dl, ffmpeg

## 設定

設定檔路徑: `/Users/nick/.config/youtube-dl/conf`

範例:

```sh
# Lines starting with # are comments
# Encode the video to another format if necessary (currently supported: mp4|flv|ogg|webm|mkv|avi)
## --recode-video 'FORMAT'

# Give these arguments to the postprocessor
## --postprocessor-args ARGS

# Keep the video file on disk after the post-processing; the video is erased by default
## -k, --keep-video

# Do not overwrite post-processed files; the post-processed files are overwritten by default
## --no-post-overwrites

# 新增ID3標籤
--add-metadata

# 以縮圖作為封面
--embed-thumbnail

# youtube
#--youtube-skip-dash-manifest

# 不要有.part
#--no-part

# Always extract audio 只取音頻
#-x

# Do not copy the mtime
--no-mtime

# Use this proxy
#--proxy 127.0.0.1:3128

# Save all videos under Movies directory in your home directory
#-o ~/Movies/%(title)s.%(ext)s
# 儲存路徑與檔名格式
-o /Users/nick/youtube-dl/%(title)s.%(ext)s
```
