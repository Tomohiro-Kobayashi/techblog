+++
title = 'WSL2 Hack'
date = 2024-01-22T18:06:54+09:00
draft = false
description = "WSL2を便利にするためのTips集"
image = "/techblog/images/common/noimage.webp"
imageBig = "/techblog/images/common/noimage.webp"
categories = ["Windows", "WSL2", "CLI"]
authors = ["Tomohiro"]
avatar = "/techblog/images/common/icon.webp"
+++

## ショートカット

### WSLからWindowsのフォルダを開く
WSL2のCLIコマンドでWindwosのフォルダを開く方法  
.zshrcに下記のエイリアスコマンドを設定。(bashの場合は.bashrc)  
open でフォルダを開く

```cl
alias open='/mnt/c/windows/explorer.exe .
```