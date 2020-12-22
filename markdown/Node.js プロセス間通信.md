# Node.jsのプロセス間通信について

## 目次

<!-- TOC depthFrom:2 -->

- [目次](#目次)
- [Node.jsはシングルプロセスで動作する。](#nodejsはシングルプロセスで動作する)
- [シングルプロセスだからこその問題もある。](#シングルプロセスだからこその問題もある)
- [プロセス間通信のやり方](#プロセス間通信のやり方)
    - [socket.ioをインストールする](#socketioをインストールする)
    - [サーバー側の実装例](#サーバー側の実装例)
    - [クライアント側の実装例](#クライアント側の実装例)

<!-- /TOC -->

## Node.jsはシングルプロセスで動作する。

今まで一般的だった「Apache」は1ユーザーに対して1プロセスが立ち上がるので、接続数が増えるとプロセスが増え、結果的にCPUはそれほどでもないのにメモリを食いつぶして遅くなる現象が起きます。

この現象はクライアント（Client）が10K（10000）を超えた時に発生する事から「C10K問題」と言われています

その対策としてNode.jsが有力です。

Node.jsは1プロセスで動作し、接続数が多くなってもプロセス数が増えないので、C10K問題が発生しません。

## シングルプロセスだからこその問題もある。

と、ここまでであればApacheよりも優秀だと思われがちですが、Node.jsにも問題はあります。

Node.jsは1プロセスでしか動作しないため、負荷の高い処理を実行するとパフォーマンスが低下するという問題があります。

その問題を解決するためにNode.jsではプロセス間通信という仕組みがあり、複数のNode.jsのプロセス間で通信が可能になっています。

## プロセス間通信のやり方

WebSocketを使ったプロセス間通信を使うには「Socket.io」モジュールを使用します。

仕組みとしてはWEBサーバーを立ち上げて、サーバーとクライアント間でWebSocket通信を確立して、通信するという感じです。

### socket.ioをインストールする

```
npm install socket.io --save
npm install socket.io-client --save
```

`socket.io`と一緒にクライント用モジュールの`socket.io-client`もインストールしておく。
サーバーには`socket.io`を使い、クライアントには`socket.io-client`を使う。

### サーバー側の実装例

```
// ①サーバ作成
var io = require("socket.io")(8080);

// ②クライアント接続があると、以下の処理をさせる。
io.on("connection", function(socket) {
  // ③接続通知をクライアントに送信
  io.emit("sendMessageToClient", { value: "[Server]:Connected!" });
  console.log("[notice]:Connected!");

  // ④クライアントからの受信イベントを設定
  socket.on("sendMessageToServer", function(data) {
    io.emit("sendMessageToClient", { value: "[Server]:Data Received!" });
    console.log("------------------------------");
    console.log("[notice]:Data Received!");
    console.log(data.value);
    console.log("------------------------------");
  });

  // ⑤接続切れイベントを設定
  socket.on("disconnect", function() {
    io.emit("sendMessageToClient", { value: "[Server]:Disconnected" });
    console.log("[notice]:Disconnected");
  });
});
```

①まずはサーバーを作成します。
requireするときにポート番号を渡すと勝手に作ってくれます。

②クライアントから接続があった時に`connection`が実行されます。

③`connection`が実行された時にクライアントにメッセージを送信しています。
ここはなくても動きますが、接続できた時になんか動いたほうがわかりやすいので入れています。

`io.emit("sendMessageToClient",{value:"メッセージ"});`でメッセージをクライアントに送信可能です。
valueの部分には変数も指定可能なので、なんか処理したデータを連携するとかにも使えます。

クライアント側にはメッセージを受け取った時に動作する関数を作っておかないと動きません。

④クライアントから送信されたデータを受け取る
クライアントから送信されたデータを受け取ります。
`socket.on("sendMessageToServer", function(data) {`の後にデータを受け取ったときの動きを書きます。
`function()`で指定した変数にもらったデータを入れられるので、今回は`data`に入れています。

その後`data.value`で中身をコンソールへ表示しています。

`sendMessageToServer`でデータを受け取ったら`sendMessageToClient`で「データを受け取ったよ！」とクライアント側に通知しています。
これは正直いりません。ちゃんと受け取れたかわかりやすいように入れています。

⑤WebSocketが切断された時に実行される処理です。
この例ではクライアントにメッセージを送信します。
「切断されたとき」という条件なので、メッセージが正常に送られることはありませんが、一応入れています。

一般的なのは切断されたときには再接続するとか、保持していたデータを消すとかそういう感じの後処理かな？

### クライアント側の実装例

```
const io = require("socket.io-client");
var socket = io.connect(URL);

// ①サーバへログテキストを送信
socket.emit("sendMessageToServer", { value: Log_Text });

// ②サーバから受け取るイベントを作成
socket.on("sendMessageToClient", function(data) {
  console.log(data.value);
});
```

すごく適当に最低限な実装がこんな感じ。

クライアント側には`socket.io-client`というモジュールを使う。

①サーバーにデータを送る処理
`Log_Text`という変数に送りたいデータが入っているので、valueとして指定して送っています。
サーバー側と特に違いはないので省略。

②サーバーから受け取るメッセージをコンソールに表示
`socket.on("sendMessageToClient", function(data) {`の後にデータを受け取ったときの処理を書いている。
今回はコンソールに受け取った内容を表示するだけ。
サーバー側と特に違いはないので省略。

**サーバーはsocket.io**を使うが、**クライアントはsocket.io-client**を使う点だけ注意。

