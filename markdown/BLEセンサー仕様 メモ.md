# BLEセンサーの仕様 メモ

## 目次

<!-- TOC depthFrom:2 -->

- [目次](#目次)
- [BLEを利用したIoTセンサー](#bleを利用したiotセンサー)
- [BLEを利用してブロードキャストする仕組み](#bleを利用してブロードキャストする仕組み)
- [BLEを使うためのライブラリとか](#bleを使うためのライブラリとか)
    - [Bluez](#bluez)
    - [Noble](#noble)
    - [bleno](#bleno)
- [センサーの設定を変更するアプリ](#センサーの設定を変更するアプリ)
- [仕様とか色々](#仕様とか色々)

<!-- /TOC -->

## BLEを利用したIoTセンサー
Bluetoothの省電力規格「Bluetooth Low Energy」（通称 BLE）を利用したIoTセンサー

国内ではレンジャーシステムズが製造・販売してるっぽい。

[monoコネクト BLE \- MVNOやIoTサービスの企画・提案・構築・運用・保守ならレンジャーシステムズ（東京都港区新橋）](https://ranger-systems.co.jp/service/visualization/mono-connect-ble/)

もともとは台湾の「INGICS Technology」が製造してるっぽい？
レンジャーシステムズが販売しているやつはOEM品？

AlibabaやAliexpressなんかの中華系ECサイトでも結構売ってる。

[INGICS \| BLE Sensor Beacon / Tag](https://www.ingics.com/tag.html)

## BLEを利用してブロードキャストする仕組み

今回のIoT検証で使ってる「iBS01H」はBluetoothの電波を利用して、情報をブロードキャストするタイプのセンサー。

BLE対応機器の中にはコネクションを確立してからデータをやり取りするタイプのセンサーも存在する。
ウェザーニュースが配布？していた温湿度などを測ることができるBLEセンサーはコネクションを確立してからやり取りするタイプ。

## BLEを使うためのライブラリとか

### Bluez
Linux系で使えるツール？
Linux系のOSに元から入ってるっぽい。

バージョンが古いこともあるので、手動でアップデートする必要がある場合も。

### Noble
Node.jsで使えるライブラリ。
Node + BLEで「Noble」。
直訳すると「貴族」「高貴な」と言った意味。

Node.jsでBLEを受信するためのライブラリ

### bleno
Node.jsで使えるライブラリ。
BLE + Nodeで「bleno」。

こっちはNode.jsでBLEを送信するためのライブラリ。
Raspberry Piを使ってビーコンを作ったりする時に使う。

## センサーの設定を変更するアプリ
センサーは基本的にセンサー情報を載せたパケットをブロードキャストしているだけだが、ボタンを押しながら電源を入れることでペアリング可能となる。

Androidアプリでセンサーの設定を変更でき、定期的に発信する状態を知らせるパケットの頻度や、送信強度なんかを弄れる。

[iBS01 Tag Utility \- Google Play のアプリ](https://play.google.com/store/apps/details?id=com.ingics.tag.igstagconfig)

## 仕様とか色々
基本的な仕様なこのページを参照。
[Sensor\_Beacon\_iBS01\_Specification\.pdf](chrome-extension://mhjfbmdgcfjbbpaeojofohoefgiehjai/index.html)

ブロードキャストしてるパケットの中身のどのビットがなんのデータを表しているかとかはPayload Formatを参照。
[iBS01\_payload\_format\.pdf](chrome-extension://mhjfbmdgcfjbbpaeojofohoefgiehjai/index.html)

各種センサーの情報と全センサーに内蔵されているボタンの押下状況、バッテリーの残量とかを検知できる。