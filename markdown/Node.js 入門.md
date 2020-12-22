# Node.js入門

## 目次

<!-- TOC depthFrom:2 -->

- [Node.js入門](#nodejs入門)
  - [目次](#目次)
  - [Node.jsとは](#nodejsとは)
    - [C10K問題とは](#c10k問題とは)
  - [Node.jsのメリット・デメリット](#nodejsのメリットデメリット)
    - [メリット](#メリット)
    - [デメリット](#デメリット)
  - [インストール](#インストール)
    - [Linux](#linux)
    - [Windows](#windows)
  - [基本的な使い方](#基本的な使い方)
  - [Node.jsのプロジェクト](#nodejsのプロジェクト)
  - [Node.jsのバージョン管理システム](#nodejsのバージョン管理システム)
  - [npmのプロキシ設定](#npmのプロキシ設定)

<!-- /TOC -->

<div style="page-break-before:always"></div>

## Node.jsとは

![Node.js ロゴ](./images/Node.js_logo.svg)

本来ブラウザで動的処理を実行するために使われるJavaScriptをサーバーサイドでも動くようにしちゃおうという思想の仕組み。

ライブラリやフレームワークと言われることがあるが、Node.jsだけでサーバーを作ったりしてHTTPリクエストを受け付けたり、レスポンスを返したり出来るので、正確には「プラットフォーム」と言うのが正しいかもしれない。

WEBサーバー特有の「C10K問題」が発生せず、大規模なシステムに向いている。

### C10K問題とは

C10K問題とは、クライアントが10K（10000）を超えるとCPUなどのハードウェア性能に余裕があってもパフォーマンスが著しく低下する現象。

最も一般的なWEBサーバー「Apache」ではクライアント1つに対してプロセスが1つ生成される。
そのため、プロセスが増えれば増えるほどRAMを消費し、結果的にCPUは使われていないのに、RAMが食いつぶされる現象が起きる。

さらに、同期処理で動作するためI/Oが多いとI/O処理待ちとなり、処理速度が低下する。

ApacheのC10K問題を解決すべく開発されたWEBサーバーが「Nginx」（エンジンエックス）で、I/Oの多重化により、1プロセスで多数のクライアント接続を処理することが可能。

<div style="page-break-before:always"></div>

## Node.jsのメリット・デメリット

### メリット

- C10K問題が発生しない
  - Node.jsはシングルスレッドで動作するため、クライアントが増えてもRAMを食いつぶさない
- ノンブロッキングI/O
  - I/O処理が非同期で読み書きが完了したタイミングでコールバック関数が呼ばれることでI/Oを実現している
- リアルタイム通信が楽
  - Socket.IOというライブラリを使うことで簡単にリアルタイム通信が可能

### デメリット

- デプロイが面倒
  - デプロイ時はプロセスの再起動が必要なので、サーバーを一時的に止める必要がある
- 人材不足
  - 実務経験がある人は少ない

<div style="page-break-before:always"></div>

## インストール

今回はLinux (Debian)環境にインストールすることを前提に話をすすめる。

### Linux

`sudo apt update`
まずはパッケージ情報のアップデートをしておく。

```
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt-get install -y nodejs
```

ちなみにmacOSにはデフォルトで入ってるらしい

[Raspberry Pi 3 Model Bに最新のNode\.jsとnpmをインストールする\[公式準拠\] \- Qiita](https://qiita.com/Avocado/items/512f64428545bf0d94ba)

### Windows
一応Windows環境でのインストール方法も書いとく。

Windowsの場合は公式サイトからインストーラーを取ってきてインストールする。

[windows10にNode\.jsをインストールする \- Qiita](https://qiita.com/Masayuki-M/items/840a997a824e18f576d8)

<div style="page-break-before:always"></div>

## 基本的な使い方

[Node\.js の基本的な使い方 · GitBook](https://hatena.github.io/Hatena-Textbook-JavaScript/nodejs/node-and-npm.html)

このあたりを参考にする。

Node.jsにはプロジェクトという概念があるようで、複雑なことをするときはプロジェクト管理が必要っぽい。

## Node.jsのプロジェクト

外部ライブラリの呼び出しなんかをする時は実行ファイル郡をプロジェクトにする必要がある。

プロジェクトにする時は、プロジェクト化したいフォルダーで以下のコマンドを実行。

```
npm init -y
```

これでプロジェクトとして扱えるようにしてくれる。
生成された`package.json`にプロジェクト名、バージョン、依存npmパッケージなんかが記録される。

必要なnpmパッケージを以下のコマンドでインストール。

```
npm install [パッケージ名]
```

必要なパッケージがインストールできれば動くはず。

インストール時に`--save`オプションを付けることでpackage.jsonに依存パッケージとして追記される。

```
npm install [パッケージ名] --save
```

[npmとpackage\.jsonが良く分からなかったので独自目線で纏めた \- Qiita](https://qiita.com/aya_akatsuki/items/f70d0d1668ef867f7256)

[Raspberry Pi 3 Model Bに最新のNode\.jsとnpmをインストールする\[公式準拠\] \- Qiita](https://qiita.com/Avocado/items/512f64428545bf0d94ba)

## Node.jsのバージョン管理システム

Node.jsはバージョンによって結構違うみたいで、Node.js自体のバージョンを管理できるnvmというバージョン管理システムがある。

これをインストールすることで簡単にNode.jsのバージョンを切り替えたりできる。

```
nvm install [バージョン]
```
で違うバージョンをインストールできる。

```
nvm use [バージョン]
```
でバージョンの切り替えが可能。

```
nvm ls
```
インストール済みのバージョン一覧を表示。

```
nvm ls-remote
```
インストール可能なバージョン一覧を表示。

かなり便利。

[node\.jsのバージョンアップ、バージョン切り替え \- Qiita](https://qiita.com/strsk/items/925644e124efcc964625)

## npmのプロキシ設定

npmを使おうと思ったらプロキシの設定が出来てなくて出来なかった。

デフォルトでは`HTTP_PROXY`か`http_proxy`の値を見に行くらしい。
npm自体に設定するには以下のコマンドで設定する。

```
npm config set proxy http://proxy.example.com:8080
npm config set https-proxy http://proxy.example.com:8080
```

[proxy環境下でのnpm config設定 \- Qiita](https://qiita.com/tenten0213/items/7ca15ce8b54acc3b5719)

