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
