# Java メモ

## 目次

<!-- TOC depthFrom:2 -->

- [目次](#目次)
- [ジェネリクス（Generics 総称型）](#ジェネリクスgenerics-総称型)
- [Enum（列挙型）](#enum列挙型)

<!-- /TOC -->

<div style="page-break-before:always"></div>

## ジェネリクス（Generics 総称型）

>ジェネリクスとは「<>」記号で囲まれたデータ型名をクラスやメソッドに付けることで、Integer型やString型などの様々な型に対応する汎用的なクラスやメソッドを作る機能のことです。

ジェネリクスそのものは 「<>」← これ

「Integer」とか「String」とかを入れて型名を明示的に記載する。

これは他から使われるクラスとかメソッドを書く時に必要な知識で、受け取るデータ型を指定しておくことで、データ型の不一致を防ぐことが出来る。


```
class ClassSample<T>{
    private T t;

    public ClassSample(T t){
        this.t = t;
    }

    public T getT(){
        return t;
    }
}

public class Main {

    public static void main(String[] args) {
        // String型として利用可能
        ClassSample<String> cs1 = new ClassSample<String>("Hello");
        String str = cs1.getT();
        System.out.println(str);

        // Integer型として利用可能
        ClassSample<Integer> cs2 = new ClassSample<Integer>(1);
        Integer i = cs2.getT();
        System.out.println(i);
    }

}
```

ジェネリクスで使えるワイルドカード的なもので`<?>` `<T>`などがある。

`<?>`はどんなデータ型でもOKという意味で、`<T>`はオブジェクト型であればなんでもOKという意味。

その他には「extends」や「super」を使うことも出来る。

「xxx型を継承したクラスであればOK」という条件も使うことが出来る。

[【Java入門】ジェネリクス\(Generics・総称型\)の使い方 \| 侍エンジニア塾ブログ（Samurai Blog） \- プログラミング入門者向けサイト](https://www.sejuku.net/blog/22699)

<div style="page-break-before:always"></div>

## Enum（列挙型）

簡単に言うと定数の集まり。
複数の定数をまとめて管理できる型。

```
public class Main {

    public static void main(String[] args) {
        Fruit fruit_type = Fruit.Orange;

        System.out.println(fruit_type);
    }

    protected enum Fruit {
        Orange,
        Apple,
        Melon
    };

}
```

enum型で定数を列強することで、`Fruit.Orange`と言った具合に定数を簡単に指定できる。

定数はenumで宣言しないとダメなわけではないが、enumで宣言すると次のような利点がある。

- メンテナンス性の向上
  - 定数を一箇所にまとめることで、機能追加時は見るべき箇所が減る。
- Javaの処理での書き換え防止
  - enumで定数を宣言すると、enumの中身を人の手で変えない限りは定数は変わらない。
- コーディング時のミス削減
  - コーディング時に定数名を入力する時に間違ったものを入力するとエラーが表示され、ミスに気づける。
- valuesメソッドを使って全ての定数を取得できる
  - 「入力された値が定数に入っている値と同じか」などの比較が簡単にできる。
- valueOf メソッドを使って定数の中から列挙子名を取得することが出来る
  - 「入力された値が指定の定数と同じか」などの比較が簡単にできる。

起動のたびに変わる定数（IPアドレス、ファイルパス、起動オプションなど）はフィールド内に定義し、モードの選択などのプログラムの実行環境に左右されない不変な定数はenumを使用すると良い。


[【Java入門】Enum\(列挙型\)の使い方総まとめ \| 侍エンジニア塾ブログ（Samurai Blog） \- プログラミング入門者向けサイト](https://www.sejuku.net/blog/14779)

<div style="page-break-before:always"></div>