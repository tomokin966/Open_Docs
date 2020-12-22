# chocolateyが便利すぎる

## 目次

<!-- TOC depthFrom:2 -->

- [chocolateyが便利すぎる](#chocolateyが便利すぎる)
  - [目次](#目次)
  - [chocolateyって何？](#chocolateyって何)
  - [chocolateyのインストール](#chocolateyのインストール)
  - [使い方](#使い方)
    - [インストール](#インストール)
    - [アンインストール](#アンインストール)
    - [アップデート](#アップデート)
    - [インストールしているパッケージすべてをアップデート](#インストールしているパッケージすべてをアップデート)
    - [chocolatey自体のアップデート](#chocolatey自体のアップデート)
    - [インストールしているソフトの一覧](#インストールしているソフトの一覧)
    - [ソフトの検索](#ソフトの検索)
    - [入手可能なすべてのバージョンを表示](#入手可能なすべてのバージョンを表示)
    - [バージョンを指定してインストール](#バージョンを指定してインストール)
    - [強制インストール、強制アンインストール](#強制インストール強制アンインストール)
    - [インストールディレクトリの指定](#インストールディレクトリの指定)
  - [提供されているパッケージ一覧](#提供されているパッケージ一覧)
  - [XMLから一括インストール](#xmlから一括インストール)
  - [GUIバージョンのインストール](#guiバージョンのインストール)

<!-- /TOC -->

<div style="page-break-before:always"></div>

## chocolateyって何？

<img src="./images/logo_square.svg" width="300px">

Windows向けのパッケージ管理ソフト。
いろんなソフトをコマンドで簡単に管理できる。

インストール、アンインストール、アップデート、特定バージョンのインストールとかもコマンドで出来るので、管理しやすい。

Chocolateyで管理している、すべてのソフトのアップデートもなんかもコマンドで出来る。

## chocolateyのインストール
以下のコマンドを、管理者権限で開いた「コマンドプロンプト」か「Windows PowerShell」で叩くだけ。
```
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```

<div style="page-break-before:always"></div>

## 使い方

「コマンドプロンプト」か「Windows PowerShell」からchocolateyのコマンドで使える。
GUI版もインストール可能だが、基本的にコマンドで操作する。

### インストール

`choco install [パッケージ名]`
`cinst [パッケージ名]`

※スペース区切りで複数パッケージの同時インストールも可能
`choco install [パッケージ名1] [パッケージ名2]`
`cinst [パッケージ名1] [パッケージ名2]`

※`--yes`か`-y`をつけると確認が表示されない

### アンインストール

`choco uninstall [パッケージ名]`
`cuninst [パッケージ名]`

### アップデート

`choco upgrade [パッケージ名]`
`cup [パッケージ名]`

### インストールしているパッケージすべてをアップデート

`choco upgrade all`
`cup all`

※`--yes`か`-y`をつけると確認が表示されない

### chocolatey自体のアップデート

`choco upgrade chocolatey`

### インストールしているソフトの一覧

`choco list -lo`
`clist -lo`

### ソフトの検索

`choco list [検索ワード]`
`clist [検索ワード]`

### 入手可能なすべてのバージョンを表示

`choco list [パッケージ名] -allversions`

### バージョンを指定してインストール

`choco install [パッケージ名] --version [バージョン]`
`cinst [パッケージ名] --version [バージョン]`

### 強制インストール、強制アンインストール

`--force`

### インストールディレクトリの指定

`-ia '/dir=[ディレクトリ]'`

<div style="page-break-before:always"></div>

## 提供されているパッケージ一覧

公式サイトにパッケージ一覧が載っている。

[Chocolatey Gallery \| Packages](https://chocolatey.org/packages)

開発に必要なものも結構ある。

最新以外のバージョンを使う時にすごく便利。

例）TensorFlow用にPython 3.6を入れたい

`choco install python --version 3.6.8`

## XMLから一括インストール

xml形式のファイルを作って一括でインストールすることも出来る。

```
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="GoogleChrome" />
    <package id="Everything" />
    <package id="winmerge" />
    <package id="SublimeText3" />
    <package id="SublimeText3.PackageControl" />
</packages>
```

こんな感じのxmlを作って・・・

`choco install [ファイルパス]`

みたいな感じで読み込ませると一括でインストールしてくれる。

<div style="page-break-before:always"></div>

## GUIバージョンのインストール

`choco install chocolateygui`

基本的にコマンドで出来ることと変わりないらしい。
ただし、GUIの持つ「エクスポート機能」はコマンドでは出来ない。

```
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="chocolatey" version="0.9.9.11" />
  <package id="ChocolateyGUI" version="0.13.1" />
  <package id="PowerShell" version="4.0.20141001" />
</packages>
```

こんな感じのxmlを出力出来るらしい。

これをさっきの「XMLファイルからの一括インストール」の手順で一括インストールすれば、環境移行が楽。