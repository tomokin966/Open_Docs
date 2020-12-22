# AndroidアプリをPlayストアに登録するための手順

## Google Play デベロッパーアカウントを作成する
Googleアカウントでログイン後に以下ページにアクセス。
[Google Play Console](https://play.google.com/apps/publish/signup/)

規約に同意後、デベロッパー登録料として**25USD**を支払う。
支払いは**1度限り**で、毎年払う必要はない。

## ストア掲載に必要な情報

- 署名されたAPKファイル
- アプリのタイトル
- 簡単な説明文 (80文字以内)
- 詳しい説明文 (4000文字以内)
- スクリーンショット (最低2枚、JPEGまたは24bit PNG<sup>[1](#note1)</sup>、1辺が320px以上 3840px以下)
- 高解像度アイコン (512x512pxの32bit PNG<sup>[2](#note2)</sup>、Google Play上で表示されるアイコン)
- ヘッダー画像 (横1024 x 縦500、JPEGまたは24bit PNG<sup>[1](#note1)</sup>)
- アプリ分類 (アプリ or ゲーム)
- カテゴリー
- コンテンツのレーティング
- 連絡先 (メールアドレス (必須)、ウェブサイト、電話番号)
- プライバシーポリシー
- 主な対象が子供かどうか
- 広告を含むかどうか

<small id="note1">[1] 24bit PNGとは、アルファ(透明度情報)なしのPNGのことである。</small>
<small id="note2">[2] 32bit PNGとは、アルファ(透明度情報)ありのPNGのことである。</small>

## 確認しなければ行けない事項
Googleが定めるプライバシーポリシーや米国輸出法などを遵守する必要があります。

- [デベロッパー ポリシー センター](https://play.google.com/intl/ja/about/developer-content-policy)
- [輸出法の遵守 \- Play Console ヘルプ](https://support.google.com/googleplay/android-developer/answer/113770?hl=ja)

## 参考URL
[\[Android\] アプリを Google Play Console に登録する](https://akira-watson.com/android/developer-console.html)
[アプリをアップロードする \- Play Console ヘルプ](https://support.google.com/googleplay/android-developer/answer/113469)