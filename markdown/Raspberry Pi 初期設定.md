# Raspberry Pi 初期設定

## 目次

<!-- TOC depthFrom:2 -->

- [Raspberry Pi 初期設定](#raspberry-pi-初期設定)
  - [目次](#目次)
  - [OSをインストール](#osをインストール)
  - [aptのプロキシ設定](#aptのプロキシ設定)
    - [etc/apt/apt.conf を作成](#etcaptaptconf-を作成)
    - [apt.conf にapt用のプロキシ設定を追記](#aptconf-にapt用のプロキシ設定を追記)
  - [シェルのプロキシ設定を追記](#シェルのプロキシ設定を追記)
  - [Chromiumにプロキシの設定をする](#chromiumにプロキシの設定をする)
  - [Mavenのプロキシ設定](#mavenのプロキシ設定)
  - [エイリアスの設定](#エイリアスの設定)

<!-- /TOC -->

<div style="page-break-before:always"></div>

## OSをインストール
RaspbianのGUI版を前提に話を進めていく。

まずはよしなにOSをインストール。

## aptのプロキシ設定

### etc/apt/apt.conf を作成
`sudo touch /etc/apt/apt.conf`

作成したら一時的にパーミッションを変更。
`sudo chmod 777 /etc/apt/apt.conf`

### apt.conf にapt用のプロキシ設定を追記
```
Acquire::http::proxy "http://proxy.example.com:8080";
Acquire::https::proxy "http://proxy.example.com:8080";
Acquire::ftp::proxy "http://proxy.example.com:8080";
```

普通にファイルブラウザーからファイルを開いて、追記する。
めんどくさければ下記コマンドでもOK。

```
echo 'Acquire::http::proxy "http://proxy.example.com:8080";' | sudo tee -a /etc/apt/apt.conf
echo 'Acquire::https::proxy "http://proxy.example.com:8080";' | sudo tee -a /etc/apt/apt.conf
echo 'Acquire::ftp::proxy "http://proxy.example.com:8080";' | sudo tee -a /etc/apt/apt.conf
```

追記が終わったらパーミッションを戻す
`sudo chmod 644 /etc/apt/apt.conf`

<div style="page-break-before:always"></div>

## シェルのプロキシ設定を追記
```
export http_proxy=http://proxy.example.com:8080
export https_proxy=http://proxy.example.com:8080
export ftp_proxy=http://proxy.example.com:8080
```
普通にファイルブラウザーからファイルを開いて、ユーザーのホームディレクトリ配下にある「.bashrc」に追記する。
デフォルトだと隠しファイルが非表示になっているので表示したければ「表示」→「隠しファイルを表示する」で隠しファイルを表示するように設定を変更する。

めんどくさければ下記コマンドでもOK
```
cd ~
echo "export http_proxy=http://proxy.example.com:8080" >> .bashrc
echo "export https_proxy=http://proxy.example.com:8080" >> .bashrc
echo "export ftp_proxy=http://proxy.example.com:8080" >> .bashrc
```

## Chromiumにプロキシの設定をする
`export CHROMIUM_FLAGS="$CHROMIUM_FLAGS --proxy-server="proxy.example.com:8080""`
ユーザーのホームディレクトリ配下にある「.profile」に追記する。

<div style="page-break-before:always"></div>

## Mavenのプロキシ設定

`mvn -v`
Mavenのホームディレクトリを表示する

```
Apache Maven 3.6.1 (d66c9c0b3152b2e69ee9bac180bb8fcc8e6af555; 2019-04-05T04:00:29+09:00)
Maven home: /opt/apache-maven-3.6.1
Java version: 1.8.0_212, vendor: Raspbian, runtime: /usr/lib/jvm/java-8-openjdk-armhf/jre
Default locale: ja_JP, platform encoding: UTF-8
OS name: "linux", version: "4.14.98-v7+", arch: "arm", family: "unix"
```

`Maven home: /opt/apache-maven-3.6.1`がホームディレクトリ

Maven home:以下、conf/setting.xml の以下を編集

```
<proxies>
    <!-- proxy
    | Specification for one proxy, to be used in connecting to the network.
    |
    <proxy>
        <id>optional</id>
        <active>true</active>
        <protocol>http</protocol>
        <username>proxyuser</username>
        <password>proxypass</password>
        <host>proxy.host.net</host>
        <port>80</port>
        <nonProxyHosts>local.net|some.host.com</nonProxyHosts>
    </proxy>
    -->
</proxies>
```

コメントを外して必要な項目をカキカキ
弊社の場合はこんな感じ

```
<proxies>
    <proxy>
        <id>optional</id>
        <active>true</active>
        <protocol>http</protocol>
        <host>proxy.example.com</host>
        <port>8080</port>
        <nonProxyHosts>192.168.*|172.25.*</nonProxyHosts>
    </proxy>
</proxies>
```
※usernameとpasswordは必要なければタグごと消してもOK

参考ページ
[Mavenが会社のプロキシに阻まれて動かないとき \- Qiita](https://qiita.com/shibafu/items/6a9e35ce7a681b8e676f)
[mavenのプロキシ設定 \- Qiita](https://qiita.com/taito-ITO/items/9763e7b3618b46691c83)

## エイリアスの設定

まずは`.bashrc`の`# some more ls aliases`下の設定郡のコメントアウトを取る。

```
if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi
```
って感じの記述があれば`.bash_aliases`も読み込んでくれるから、システムに標準として書き込まれているやつ以外を追加する時は`.bash_aliases`に分離したほうが良さそう。

以下が`.bash_aliases`に設定したエイリアス一覧

```
alias cat='cat -n'
alias dateset='sudo date --set @"$(wget -q https://ntp-a1.nict.go.jp/cgi-bin/jst -O - | sed -n 4p | cut -d. -f1)"'
alias df='df -h'
alias update='sudo apt update'
alias upgrade='sudo apt upgrade'
alias c='clear'
alias ..='cd ..'
alias bashrc='source ~/.bashrc'
```

上から説明すると
- cat : `cat`するときに行番号を表示するオプション（-n）をつける
- dateset : NTP系のコマンドが使えないプロキシ環境下で時間を合わせるためのコマンド
- df : `df`するときに見やすい単位（MBとかGBとか）で表示するためのオプション（-h）をつける
- update : `sudo apt update`するのが面倒なので短縮
- upgrade : `sudo apt upgrade`するのが面倒なので短縮
- c : コンソールをクリアする`clear`コマンドの短縮
- .. : `cd ..`の短縮
- bashrc : `.bashrc`を再読み込みするコマンドの短縮

[よく設定されているalias \- Qiita](https://qiita.com/hirooooooo/items/5c47fdaf40fc1d3b702f)
[個人的によく使う（ベタな）bash alias \- Qiita](https://qiita.com/Cj-bc/items/95de01ca66d8367d611f)