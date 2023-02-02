## 記事

[自然発生した実装パターンにマイクロフロントエンドと名がつきました](https://speakerdeck.com/berlysia/jsconf-jp-2022)
[エンジニアコース新人研修の内容を公開します！](https://blog.recruit.co.jp/rtc/2021/08/20/recruit-bootcamp-2021/)

## TypeScript

[ブラウザでいろんなバージョンの JS を動かせるサイト](https://www.typescriptlang.org/play?#code/PTAEHUFMBsGMHsC2lQBd5oBYoCoE8AHSAZVgCcBLA1UABWgEM8BzM+AVwDsATAGiwoBnUENANQAd0gAjQRVSQAUCEmYKsTKGYUAbpGF4OY0BoadYKdJMoL+gzAzIoz3UNEiPOofEVKVqAHSKymAAmkYI7NCuqGqcANag8ABmIjQUXrFOKBJMggBcISGgoAC0oACCbvCwDKgU8JkY7p7ehCTkVDQS2E6gnPCxGcwmZqDSTgzxxWWVoASMFmgYkAAeRJTInN3ymj4d-jSCeNsMq-wuoPaOltigAKoASgAywhK7SbGQZIIz5VWCFzSeCrZagNYbChbHaxUDcCjJZLfSDbExIAgUdxkUBIursJzCFJtXydajBBCcQQ0MwAUVWDEQC0gADVHBQGNJ3KAALygABEAAkYNAMOB4GRonzFBTBPB3AERcwABS0+mM9ysygc9wASmCKhwzQ8ZC8iHFzmB7BoXzcZmY7AYzEg-Fg0HUiQ58D0Ii8fLpDKZgj5SWxfPADlQAHJhAA5SASPlBFQAeS+ZHegmdWkgR1QjgUrmkeFATjNOmGWH0KAQiGhwkuNok4uiIgMHGxCyYrA4PCCJSAA)

## React

[useEffect 完全ガイド](https://overreacted.io/ja/a-complete-guide-to-useeffect/)

## CSS

https://developer.mozilla.org/ja/docs/Learn/CSS/CSS_layout

### img タグについて

next-image を使っていないのと関連もするのですが、 img を読み込むときは、絶対に画像の高さを指定するようにしてください。

この div に出力した figma の画像の高さを height: 20px のようにベタっと書いておいて、という意味です。

img タグは、画像の読み込みが完了するまでは、その要素を何 px で表示すればいいのかブラウザも判断がつかないため、ネットワークから画像の読み込みが完了したあとに、ブラウザが高さを補正する動きになってしまいます。
(この動きを Layout Shift と呼ぶ )

ユーザーからすると、いきなり画面の構成要素が下にずれるような体験になってしまうため、「バナー画像による Layout Shift は起こしてはいけない」という鉄則があります。

Layout Shift は事前に画像の高さを知っていれば容易に防げるため、↓ のような対処を行うわけです。

この div に出力した figma の画像の高さを height: 20px のようにベタっと書いておいて、という意味です。

※ next-image を使うと、component の必須 prop に width / height が含まれるので、Layout Shift を起こさない書き方が強制される
(Layout Shift が多く発生するページは Core Web Vitals というスコアが下がり、結果として google 検索結果を下げられるような SEO ペナルティを食らうこともあるので、画像設置するときは特に要注意)

### aspect-ratio について

height: 120px; だと、window 幅縮めたときにおかしくなるから、今回は固定 height ではなく、aspect-ratio の方が良いですね。

```
margin-top: ${spacing[32]};
width: 100%;
aspect-ratio: 1136 / 120;
```

これで、「横 1136 縦 120 の比率を保つ div 」にできます。

(aspect-ratio は割と新しめの CSS 機能ですが、古いブラウザでは無視されて layout shift 発生する程度なので問題ない)
