# WinSCP

## 目次

<!-- TOC depthFrom:2 -->

- [目次](#目次)
- [公開鍵認証で接続する方法](#公開鍵認証で接続する方法)
    - [秘密鍵をコンバートする](#秘密鍵をコンバートする)
    - [接続設定に秘密鍵をセットする](#接続設定に秘密鍵をセットする)

<!-- /TOC -->

<div style="page-break-before:always"></div>

## 公開鍵認証で接続する方法

### 秘密鍵をコンバートする

1. WinSCPを起動
2. 左下「ツール」→「PuTTYgenを実行」を選択
3. 「Conversions」 → 「Import key」を選択
4. 秘密鍵を選択
5. 「Actions」の中にある「Save private key」を選択
6. 保存場所を選択して*.ppkで保存<br>(.ssh 配下に"id_rsa.pkk"って感じで保存するのがベターか？)

### 接続設定に秘密鍵をセットする

1. WinSCPを起動
2. ログイン先を選択し、画面右セッションの「編集」を選択。
3. 「設定」を選択。
4. SSH → 認証 → 認証条件の秘密鍵にさっきコンバートした秘密鍵を指定。
5. 「OK」を押して設定を完了する。
6. ログイン先選択画面になったら保存を選択。
7. ログイン！！！！！

参考ページ
[WinSCP用に秘密鍵をコンバートしてSSH接続する \- デフよん](https://def-4.com/winscp_private_key/)