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
	# "Attached"へ(WSLへ認識させる）
	usbipd attach --wsl --busid [BUSID]
	# "Attached"確認
	usbipd list
	```

2. WSL内で/dev/ttyUSB*を確認する
```bash
ls /dev/ttyUSB*
```

3. WSL内でsocatを使って/dev/ttyUSB*を中継する

	3-1. WSLに"socat"をインストール
	```bash
	sudo apt install socat
	```
	3-2. socatを使って中継を実行
	```bash
	sudo socat -d -d TCP4-LISTEN:2001,reuseaddr,fork FILE:/dev/ttyUSB0,raw,echo=0,b115200
	```
4. Docker container内でsocatを使って/dev/ttyUSB*を受信する


