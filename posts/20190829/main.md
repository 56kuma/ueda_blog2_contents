---
Keywords: 日記
Copyright: (C) 2019 Ryuichi Ueda
---

# pyというコマンドを作ったった

　本日は学科の仕事。合間にコマンドを作っていました。朝に`rb`というRubyをワンライナーで使うコマンドが便利だというツイートがあったので、Pythonで同じようなコマンドが作れないかやってみようというのがきっかけです。

　ちなみにそのツイートはブログへのリンクで、そのブログ記事はシェルのワンライナーを**レガシー呼ばわり**（*心の声: 出！出〜〜〜！！！１でた〜！いっつもレガシーとかバッドプラクティスっていうんだよあの人たち・・・*）する代物だったので、引用はしません。だけどきっかけをくれて感謝しておりますです。あんまりRuby的なものがベストプラクティスで他はバッドだと言ってると、かえってRubyを使っている人たちの評判を落とすので、やめた方がいいと思います。「ある点ではこちらが優れている」という研究者的な表現をお勧めいたします。自分もたまに「Javaは・・・」とかやらかしていましたが、今は厳に慎んでおります。私は言語、適材適所でなんでも使います。


　それはさておき、謎の高速プロトタイピングテクノロジー（注意: しかしそれで終わることが多い）で、合計2時間くらいでちょちょいと作ったものが次のような`py`というコマンドです。

## 使い方

awkのように数字と文字列を自動認識したり、フィールドをF1, F2と参照できたりと、微妙に芸が細かくなっております。が、基本、処理が大きく限定されており、行またぎの処理ができません・・・。

### awkのようなパターン

```
$ seq 10 | py 'F1%2==0'
2
4
6
8
10
```

### awkのようなアクション

```
$ echo 1 2 3 a b c | py '[ F2, F3*3, F5+"aaa"]'
2 9 baaa
```

### パターン & アクション

```
$ seq 10 | py 'F1%2==0[F1, ":even"]'
2 :even
4 :even
6 :even
8 :even
10 :even
```

### モジュールのインポート

````
$ seq 1 3 | py -m 'import math' '[ F1*math.pi, math.sin(F1) ]' 
3.141592653589793 0.8414709848078965
6.283185307179586 0.9092974268256817
9.42477796076938 0.1411200080598672
````


### リスト内包

```
$ seq 1 100 | xargs -n 10 | ./py '[ 1.0/x for x in f[1:3] ]'
1.0 0.5
0.09090909090909091 0.08333333333333333
0.047619047619047616 0.045454545454545456
0.03225806451612903 0.03125
0.024390243902439025 0.023809523809523808
0.0196078431372549 0.019230769230769232
0.01639344262295082 0.016129032258064516
0.014084507042253521 0.013888888888888888
0.012345679012345678 0.012195121951219513
0.01098901098901099 0.010869565217391304
```


コードはこちらです。

<blockquote class="twitter-tweet" data-partner="tweetdeck"><p lang="ja" dir="ltr">てきとうに機能を付け足して行ったらクソみたいになったコマンドpyのコード<a href="https://twitter.com/hashtag/%E3%82%84%E3%82%8A%E3%81%AA%E3%81%8A%E3%81%99%E3%81%B9%E3%81%8D?src=hash&amp;ref_src=twsrc%5Etfw">#やりなおすべき</a><a href="https://t.co/AQbw1cakk9">https://t.co/AQbw1cakk9</a></p>&mdash; 上田 隆一 (@ryuichiueda) <a href="https://twitter.com/ryuichiueda/status/1167076379252285441?ref_src=twsrc%5Etfw">August 29, 2019</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>


以上です。寝る。