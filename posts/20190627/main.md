---
Keywords: 日記
Copyright: (C) 2019 Ryuichi Ueda
---

# 日記（2019年6月27日）

　午前は研究で使うcartographerからのデータいじり。午後は講義で使う産業用マニピュレータ10台をTA氏と共にメンテナンス（電池を変えて原点調整）。湿気と生ぬるい空気でダウン気味。

## cartographerのデータいじり

　cartographerから[こんなふうに保存した](https://google-cartographer-ros.readthedocs.io/en/latest/assets_writer.html)地図とロボットの軌跡のデータを自分のコードで使うためのコード等を書いている。[データ](https://github.com/ryuichiueda/mapping_pfoe/blob/master/bag_and_maps/20190625_square.pbstream)はGoogleお得意のプロトコルバッファで保存されているのでデータを取り出すのがクソ面倒。自分でファイルを開くコードを書かずにcartographerに再度データを読み込ませて`map_saver`とトピックから地図と軌跡を取り出すことにした。バイナリのメリットが活きない例だと思われ。

## bashcms本の陳列が進む

　本日はジュンク堂でツイートしていただいた。

<blockquote class="twitter-tweet" data-partner="tweetdeck"><p lang="ja" dir="ltr">6/27新刊：ISBN978-4-04-893069-7 ドワンゴ 『フルスクラッチから1日でCMSを作る シェルスクリプト高速開発手法入門 改訂2版』 上田隆一、後藤大地 著　USP研究所 監修　7冊入荷 <a href="https://t.co/TIfIQMyIcI">pic.twitter.com/TIfIQMyIcI</a></p>&mdash; ジュンク堂書店 池袋本店/PC書 (@junkudo_ike_pc) <a href="https://twitter.com/junkudo_ike_pc/status/1144130834326155264?ref_src=twsrc%5Etfw">June 27, 2019</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
