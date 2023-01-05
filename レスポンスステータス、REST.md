## ドキュメント

[Faraday](https://lostisland.github.io/faraday/usage/)

## 300 系でやること

## 400 系でやること

- Sentry にログを送信する

## 500 系でやること

- Job のリトライ
- Sentry にログを送信
- 例外を発生させる、raise する

## REST

### PUT メソッド

```
updateメソッドを作って、コインを足すのも引くのもこのメソッドでやろうとしたが、冪等な観点では不適切だった。add/consumeメソッドを作ってPOSTに変更した。

以下、引用。

HTTP の PUT メソッドは、基本的に、既存の値を新しいもので上書きするという挙動が想定されます。
なので、例えば元のコインが20で、 put /coin に 30 を渡すと、所持コインが (50ではなく) 30 になるというのが想定される挙動です。

https://developer.mozilla.org/ja/docs/Glossary/Idempotent
一般的に PUT は冪等(idemponent) な HTTP メソッドと言われるのですが、その理由が上記で、何度実行しても同じ値に上書きされつづけるべきだからです。

冪等性が非常に重要な API であること (なので正しく使っておきたい)
```
