# npm 入門

## 目次

<!-- TOC depthFrom:2 -->

- [npm 入門](#npm-入門)
  - [目次](#目次)
  - [npmとは？](#npmとは)
  - [プロキシ設定](#プロキシ設定)
  - [npmコマンド](#npmコマンド)
    - [npm init](#npm-init)
    - [npm install](#npm-install)
    - [npm update](#npm-update)

<!-- /TOC -->

<div style="page-break-before:always"></div>

## npmとは？
Node.jsのパッケージを管理するためのソフト

Pythonで言うところのpipみたいなやつ

## プロキシ設定

プロキシ環境下だとそのままでは動かない。

まずはプロキシ設定からやってく。

## npmコマンド

### npm init

ディレクトリをnpm管理下に置くためのコマンド。
`package.json`とかが生成されて、パッケージで管理可能になる。

```
npm init -y
```

### npm install

パッケージ名をインストールする時に使うやつ。

```
npm install [パッケージ名]
```

`--save`オプションをつけると、インストールと同時に`package.json`に依存パッケージとして登録される。


### npm update

`package.json`に書かれている依存パッケージを自動的に取得するコマンド。

ちゃんと`package.json`を書いていれば、これだけでモジュールとかを構築できる。

```
npm update
```