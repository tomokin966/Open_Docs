# Raspberry Piのコマンドいろいろ

## 目次

<!-- TOC depthFrom:2 -->

- [目次](#目次)
- [CPU温度を調べる](#cpu温度を調べる)
- [CPUクロックを調べる](#cpuクロックを調べる)
- [電圧を調べる](#電圧を調べる)
- [CPUのメモリ消費量を調べる](#cpuのメモリ消費量を調べる)
- [GPUのメモリ消費量を調べる](#gpuのメモリ消費量を調べる)
- [定期的にコマンドを実行する(常時更新)](#定期的にコマンドを実行する常時更新)
- [ファイルの末尾を監視するコマンド](#ファイルの末尾を監視するコマンド)
- [apt系](#apt系)
    - [aptでアップデートするときの手順](#aptでアップデートするときの手順)
- [aptアップデートを自動化する](#aptアップデートを自動化する)
- [時間を合わせる](#時間を合わせる)

<!-- /TOC -->

<div style="page-break-before:always"></div>

## CPU温度を調べる
`vcgencmd measure_temp`

常に温度を調べるにはこう
`watch -n 1 -t vcgencmd measure_temp`

## CPUクロックを調べる
`vcgencmd measure_clock arm`

## 電圧を調べる
`vcgencmd measure_volts`

## CPUのメモリ消費量を調べる
`vcgencmd get_mem arm`

## GPUのメモリ消費量を調べる
`vcgencmd get_mem gpu`

<div style="page-break-before:always"></div>

## 定期的にコマンドを実行する(常時更新)
`watch [オプション] [コマンド]`

オプション
| オプション | 説明                                               |
| :--------: | -------------------------------------------------- |
|     -n     | 更新間隔、デフォルトは2秒 `-n 5`って感じで指定する |
|     -d     | 変更があった場所をハイライト                       |
|     -t     | ヘッダー情報を非表示                               |

## ファイルの末尾を監視するコマンド
`tail [オプション] [ファイル名]`

デフォルトだと末尾の10行を表示する。

オプション
| オプション | 説明                                                            |
| :--------: | --------------------------------------------------------------- |
|     -n     | 表示行数 デフォルトは10行 `-n 10`または`-n10`って感じで指定する |
|     -c     | 表示バイト数 `-c 10`って感じで指定する                          |
|     -f     | リアルタイムで監視（ファイルが更新されたら表示も更新される）    |

ログファイルとか見る時に`tail -f [ファイル名]`って感じで使うことが多い。

何気に便利なコマンド。

lessのほうが高性能らしい？
できればtailよりlessを使いこなせるようになると良いかも？
[「tail \-f」を使うのは情弱、情強は「less \+F」を使う \| ソフトアンテナブログ](https://www.softantenna.com/wp/unix/stop-using-tail-f/)

<div style="page-break-before:always"></div>

## apt系

`sudo apt update`
リポジトリ一覧を更新(リポジトリ追加・削除時には必ず実行すること)

`sudo apt upgrade`
パッケージを更新(通常のパッケージ更新時はこのコマンドを使用する)

`sudo apt full-upgrade`
パッケージを更新(保留されているパッケージを更新するときに使用する)

`sudo apt autoremove`
更新に伴い必要なくなったパッケージを削除(apt実行時にこのコマンドを実行するよう表示されたら実行する)

`sudo apt install {パッケージ名やdebファイルのパス}`
パッケージやdebファイルをインストール

`sudo apt remove {パッケージ名}`
パッケージを削除

`sudo apt remove --purge {パッケージ名}`
パッケージを完全削除

`sudo apt show {パッケージ名}`
パッケージの詳細情報を表示

`sudo apt list {パッケージ名}`
パッケージを検索(完全一致)

`sudo apt search {パッケージ名}`
パッケージを検索(部分一致)

`sudo dpkg -l`
インストール済みのパッケージ一覧を表示

`sudo dpkg -L {パッケージ名}`
パッケージのインストール先を表示

`cat /var/log/apt/history.log`
aptコマンドの使用履歴を表示

`sudo apt autoclean`
キャッシュされているが、インストールはされていないdebファイルを削除

`sudo apt clean`
キャッシュされている全てのdebファイルを削除

`echo "{パッケージ名} hold" | dpkg --set-selections`
パッケージをアップデート対象から除外

`echo "{パッケージ名} install" | dpkg --set-selections`
パッケージをアップデート対象に戻す

参考ページ
[aptコマンドチートシート \- Qiita](https://qiita.com/SUZUKI_Masaya/items/1fd9489e631c78e5b007)

<div style="page-break-before:always"></div>

### aptでアップデートするときの手順

`sudo apt update`で現在の構成情報を更新する。
これによってアップデートすべきパッケージがあるかどうかなどを取得する。

`sudo apt upgrade`で実際にアップデートを実行する。

その後再度`sudo apt update`を実行し、構成情報を更新する。
この時にすべてのパッケージが最新であれば、アップデート完了。

基本的には
```
sudo apt update
sudo apt upgrade
sudo apt update
```
の順で実行するみたい？

## aptアップデートを自動化する

アップデートを自動化するためのパッケージも存在する。
自動でアップデートさせないパッケージの指定、アップデート時にメールで通知を受けたりとかも出来るみたい。
とりあえず入れて、設定ファイルをちょっと編集すれば使える？

参考ページ
[RaspberryPiでupdate/upgradeを自動化する。 \- Qiita](https://qiita.com/Fendo181/items/659f306232f55fc5a8de)

## 時間を合わせる

プロキシ環境だとNTPとかで時間をあわせれないこともある。

プロキシ環境下でも時間を合わせられるコマンドが以下の通り。

```
sudo date --set @"$(wget -q https://ntp-a1.nict.go.jp/cgi-bin/jst -O - | sed -n 4p | cut -d. -f1)"

```

エイリアスに登録しておくと便利かも？

```
alias dateset='sudo date --set @"$(wget -q https://ntp-a1.nict.go.jp/cgi-bin/jst -O - | sed -n 4p | cut -d. -f1)"'
```

[ntpを使わずに時刻を合わせるワンライナー（Proxy環境下でも安心） \- Qiita](https://qiita.com/pankona/items/258fed78c168918a8ad2)