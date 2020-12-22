# TeraTerm

## 目次

<!-- TOC depthFrom:2 -->

- [目次](#目次)
- [自動でログインするショートカットを作る](#自動でログインするショートカットを作る)
    - [引数の解説](#引数の解説)

<!-- /TOC -->

<div style="page-break-before:always"></div>

## 自動でログインするショートカットを作る

右クリック → 新規作成 → ショートカット

ショートカット作成画面の「項目の場所を入力してください」のテキストボックスに以下を編集して貼り付け
`"C:\Program Files (x86)\teraterm\ttermpro.exe" 192.168.1.100:22 /auth=publickey /user=pi /keyfile=C:\Users\admin\.ssh\id_rsa`

### 引数の解説
`"C:\Program Files (x86)\teraterm\ttermpro.exe"`
TeraTermのインストール場所

`192.168.1.100:22`
IPアドレスとポート

`/auth=publickey`
認証方法
パスワード認証：　/auth=passwd
公開鍵認証　　：　/auth=publickey

`/user=pi`
ユーザー名

`/keyfile=C:\Users\admin\.ssh\id_rsa`
秘密鍵のディレクトリ

参考ページ
[【手順】teratermのショートカット作成方法 \- Qiita](https://qiita.com/takahashi-kazuki/items/1bf502497461bc6f285b)