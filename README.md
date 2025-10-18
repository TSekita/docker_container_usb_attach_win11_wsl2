# docker containerにusbシリアルを認識させる方法

## 環境

- Windows11

- Docker Desktop

- WSL2 Ubuntu 24.04

- Docker container Ubuntu 22.04

## 手順

1. WSLにusbシリアルを認識させる

2. WSL内で/dev/ttyUSB*を確認する

3. WSL内でsocatを使って/dev/ttyUSB*を中継する

4. Docker container内でsocatを使って/dev/ttyUSB*を受信する

## 詳細な手順(Step by Step)

1. WSLにusbシリアルを認識させる

1-1. WSLをupdateし再起動
```terminal
# WSLのupdate
wsl --update
# WSLの再起動
wsl --shutdown
wsl
```
1-2. 該当のUSBシリアルをWSLに接続
```terminal	
# 管理者権限のあるterminalやpowershellを開き実行
# 接続状況を確認
usbipd list
# 該当のUSBシリアルの"BUSID"を"Shared"へ
usbipd bind --busid [BUSID]
# "Shared"確認
usbipd list
# "Attached"へ
usbipd attach --wsl --busid [BUSID]
# "Attached"確認
usbipd list
```

2. WSL内で/dev/ttyUSB*を確認する

3. WSL内でsocatを使って/dev/ttyUSB*を中継する

4. Docker container内でsocatを使って/dev/ttyUSB*を受信する

