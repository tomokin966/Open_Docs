# Raspberry PiでBLEを使う

## 目次

<!-- TOC depthFrom:2 -->

- [目次](#目次)
- [BLEとは？](#bleとは)
- [BLEを使うために必要なパッケージをインストール](#bleを使うために必要なパッケージをインストール)
- [BlueZ本体をビルドしてインストール](#bluez本体をビルドしてインストール)
- [使い方とかその他諸々](#使い方とかその他諸々)
- [参考にしたページ](#参考にしたページ)

<!-- /TOC -->

<div style="page-break-before:always"></div>

## BLEとは？
## BLEを使うために必要なパッケージをインストール

BLEを使うためのパッケージ「BlueZ」を使うためのパッケージをインストールする。

まずはお決まりのパッケージアップデート
`sudo apt update`
`sudo apt upgrade`

前提パッケージをインストール

```
sudo apt install libusb-dev
sudo apt install libdbus-1-dev
sudo apt install libglib2.0-dev
sudo apt install libudev-dev
sudo apt install libical-dev
sudo apt install libreadline-dev
sudo apt install libdbus-glib-1-dev
sudo apt install libbluetooth-dev
```

このあたりをインストールする。

## BlueZ本体をビルドしてインストール

[BlueZ » Download](http://www.bluez.org/download/)
この辺から最新のtar.xzを探す。
2019/06/20時点では5.9が最新。

[BlueZ バージョン一覧](https://www.kernel.org/pub/linux/bluetooth)
過去のバージョンを使いたい時とか、見つからない時はこの辺を参照。

`wget https://www.kernel.org/pub/linux/bluetooth/bluez-5.9.tar.xz`
wgetでファイルをダウンロードする。

`tar xvf bluez-5.9.tar.xz`
解凍する。

`cd bluez-5.32`
ディレクトリ移動

`./configure --disable-systemd --enable-library`
configureでビルドの設定をする。

`make`
ビルドする。4コア使ってビルドしたい時は`make -j4`を使う。

## 使い方とかその他諸々

D-Busという機能を使ってBluetoothにアクセスしてるっぽい。
BlueZはD-Bus経由でデバイスを制御するためのプロトコルスタック？だそう。

Linux標準でRaspberry Piで一般的なOSである「Raspbian」でももちろん使える。
ただし、もとから入ってるやつはバージョンが古い可能性があるので、自分でビルドしてインストールしたほうが良い。

それが上の手順。

参考になるページとか
[BlueZのAPI/サンプルコードのメモ \- Qiita](https://qiita.com/ffmatsu/items/b7ca6a944b5a1ea9c7a6)
[D\-Bus のはなし｜Wireless・のおと｜サイレックス・テクノロジー株式会社](http://www.silex.jp/blog/wireless/2017/01/d-bus.html)

## 参考にしたページ
[Raspberry Pi 3でBluetooth LEを導入する \| クリブロ！](https://blog.creatorslab.jp/2017/03/18/raspberry-pi-ble-install/)

[configure, make, make install とは何か \- Qiita](https://qiita.com/chihiro/items/f270744d7e09c58a50a5)

[BlueZ](http://www.bluez.org/)