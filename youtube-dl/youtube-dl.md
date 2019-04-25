---

## youtube-dl

### 安裝

開啟終端機輸入指令 `brew install youtube-dl ffmpeg` 安裝youtube-dl, ffmpeg

### 設定檔

- 路徑 `/etc/youtube-dl.conf` 以下為設定檔範例:
- 或下載文件再置於上述路徑
  - [youtube-dl.conf](/youtube-dl.tar.gz) (MacOS)
  - [youtube-dl_moode.conf](/youtube-dl_moode.tar.gz) (moOde OS)

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

# 儲存路徑與檔名格式
-o '/Users/nick/youtube-dl/%(title)s.%(ext)s'
```