# google-images-downloadの使い方

## 目次

<!-- TOC depthFrom:2 -->

- [目次](#目次)
- [Google画像検索から画像をダウンロードするツール](#google画像検索から画像をダウンロードするツール)
- [インストール方法](#インストール方法)
- [使い方](#使い方)
- [オプション一覧](#オプション一覧)
- [100件以上のダウンロードには「ChromeDriver」が必要](#100件以上のダウンロードにはchromedriverが必要)
- [詳しい使い方とか](#詳しい使い方とか)

<!-- /TOC -->

<div style="page-break-before:always"></div>

## Google画像検索から画像をダウンロードするツール

Google検索から画像を一括でダウンロード出来る。
画像認識のモデルに学習させる時に便利。

>参考にしたページ
[Googleから画像を一括でダウンロードするツール「google\-images\-download」 \| cupOF Interests](https://co.bsnws.net/article/295)


## インストール方法
```
pip install google_images_download
```

pipでインストールする。

## 使い方
コマンドラインから簡単にダウンロード出来る。

```
googleimagesdownload --keywords "リンゴ"
```

カレントディレクトリに「リンゴ」の検索結果を100件保存。

<div style="page-break-before:always"></div>

## オプション一覧

| オプション       | ショートカット | 説明                                                                                                                                                                                                                                                                                                                                      |
| ---------------- | -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| keywords         | k              | ターゲットとなる画像のキーワード                                                                                                                                                                                                                                                                                                          |
| suffix_keywords  | sk             | キーワードを追加する為の接尾辞 ('りんご' '赤' など)                                                                                                                                                                                                                                                                                       |
| limit            | l              | 一度にダウンロードする画像数 (デフォルトでは100個)                                                                                                                                                                                                                                                                                        |
| format           | f              | ダウンロードする画像の形式 (jpg, gif, png, bmp, svg, webp, ico)                                                                                                                                                                                                                                                                           |
| color            | co             | ダウンロードする画像の色を指定 (red, orange, yellow, green, teal, blue, purple, pink, white, gray, black, brown)                                                                                                                                                                                                                          |
| color_type       | ct             | ダウンロードする画像色のタイプ (full-color, black-and-white, transparent)                                                                                                                                                                                                                                                                 |
| size             | s              | ダウンロードする画像のサイズ (large, medium, icon, >400*300, >640*480, >800*600, >1024*768, >2MP, >4MP, >6MP, >8MP, >10MP)                                                                                                                                                                                                                |
| aspect_ratio     | a              | ダウンロードする画像の形。パノラマなど(tall, square, wide, panoramic)                                                                                                                                                                                                                                                                     |
| type             | t              | ダウンロードする画像のタイプ。パノラマなど(face, photo, clip-art, line-drawing, animated)                                                                                                                                                                                                                                                 |
| time             | w              | インデックスされた画像の期間を指定 1日以内, 一週間以内など( past-24-hours, past-7-days)                                                                                                                                                                                                                                                   |
| similar_images   | si             | 指定した画像ファイルやURLから、似たイメージをダウンロードします                                                                                                                                                                                                                                                                           |
| output_directory | o              | 指定したディレクトリに画像を展開。デフォルトではコマンドを実行したディレクトリに画像がダウンロードされます                                                                                                                                                                                                                                |
| language         | la             | 画像を入手するGoogleサービスの言語を指定 (Arabic, Chinese (Simplified), Chinese (Traditional), Czech, Danish, Dutch, 　English, Estonian. Finnish, French, German, Greek, Hebrew, Hungarian,   Icelandic, Italian, Japanese, Korean, Latvianm, Lithuanian, Norwegian,   Portuguese, Polish, Romanian, Russian, Spanish, Swedish, Turkish) |
| chromedriver     | cd             | 画像を入手するドライバを chromedriverに変更できます。                                                                                                                                                                                                                                                                                     |

<div style="page-break-before:always"></div>

## 100件以上のダウンロードには「ChromeDriver」が必要

デフォルトで設定されている100件以上の画像をダウンロードするには「chromeDriver」が必要。

下記URLからダウンロード。
[Downloads \- ChromeDriver \- WebDriver for Chrome](http://chromedriver.chromium.org/downloads)

解凍して出てきた「chromedriver.exe」をカレントに置く。

```
googleimagesdownload -ri -cd "chromedriver.exe" -l 1000  -k "猫"
```
こんな感じで叩けば出来るっぽい。

## 詳しい使い方とか

GitHubのページにいろいろ書いてるからそれを参照。

[GitHub \- hardikvasa/google\-images\-download: Python Script to download hundreds of images from 'Google Images'\. It is a ready\-to\-run code\!](https://github.com/hardikvasa/google-images-download/)

英語だから読むのめんどいけど、いろいろ書いてる。