---
Keywords: プログラミング,勉強会,シェル芸,シェル芸勉強会
Copyright: (C) 2018 Ryuichi Ueda
---

# 【問題と解答】jus共催 第36回七夕・・・7は素数じゃないですか（しかも2つ）シェル芸勉強会

<!--[当日の様子はこちら](/?post=20180408_shellgei_35_summary)-->

* 問題で使われているデータファイルは[GitHub](https://github.com/ryuichiueda/ShellGeiData/tree/master/vol.36)にあります。クローンは以下のようにお願いします。

```bash
$ git clone https://github.com/ryuichiueda/ShellGeiData.git
```

* 環境: 解答例はUbuntu Linux 18.04 で作成。Macの場合はcoreutilsをインストールすると、GNUのコマンドが使えます。BSD系の人は玄人なので各自対応のこと。

<!-- もっと良い別解がたくさんありますので、 https://togetter.com/li/1216252 も参考に。-->

## Q1

`welcome.txt`に隠されたメッセージを読み取ってください。また、`welcome.txt`をワンライナーで作ってみてください。

### 解答

解読は次の通り。

```
$ cat welcome.txt | tr '\0' @ | fold -b70
________________________________________________@__@_@________________
_@@___________________________@@@@@@_______@@____@@@@@__@_____________
__@______________@______________@@_________@@_@@@@@______@____@@@_____
__@_____________@@@@@_________@@@@@@@______@______@______@__@____@____
__@_____@________@@@_________@__@@__@______@@@___@@______@@@____@@____
___@@@@@_______@@__@@@_________@@@@@________@___@@_________@__________
______________________________________________________________________
______________________________________________________________________
_________________________________@__________________________@@@_______
_______@_@________@@__________@@@@@@________________________@@@@______
__@@@@____________@@__________@@@@@@@__________@__________@@____@_____
@@____@@_________@@@____________@@@@@__________@@@______________@_____
________@@@_____@@__@___@_____@@___@@________@@@@______________@______
_______________@@___@@@@_______@@@@@________@@@@_@@__________@@_______
______________________________________________________________________
______________________________________________________________________
______________________________________________________________________
___@@___@_____@_______________________________________________________
_@@@@@@@_@@____@____@@@_______________________________________________
____@__@_@@____@__@____@______________________________________________
___@___@_______@@@____@@______________________________________________
__@__@@@_________@____________________________________________________
______________________________________________________________________
______________________________________________________________________
```

このように作りました。

```
$ figlet しぇるげいべんきょうかい | sed 's/[^ ]/@/g' |
tr ' ' _ | tr @ '\0' | tr -d '\n' > welcome.txt
```

## Q2

次のファイル群について、全てファイル名を`N年M組.doc`（`N`は半角数字、`M`は半角大文字）に揃えて徳を積んでください。

```
$ ls
1-B.doc     3年Ｃ組.doc  ３年A組.doc  １ーC.doc    ４年Ｃ組.doc
1A.doc      4年a組.doc   ３年B組.doc  １ーD.doc
3年D組.doc  5年A組.doc   ４年B組.doc  １年E組.doc
```

### 出典

<blockquote class="twitter-tweet" data-partner="tweetdeck"><p lang="ja" dir="ltr">これ最悪じゃないですか <a href="https://t.co/O2ezYAFMMK">pic.twitter.com/O2ezYAFMMK</a></p>&mdash; 漁師 (@6Lgug) <a href="https://twitter.com/6Lgug/status/1011529645559173120?ref_src=twsrc%5Etfw">June 26, 2018</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

### 解答

```
$ ls | nkf -Z4 | tr a A | sed 's/[-ｰ]/年/' |
sed 's/\([A-E]\)\./\1組./' | sed 's/1A/1年A/' |
paste <(ls) - | sed 's/^/mv /' | sh
mv: '3年D組.doc' と '3年D組.doc' は同じファイルです
mv: '5年A組.doc' と '5年A組.doc' は同じファイルです
$ ls
1年A組.doc  1年C組.doc  1年E組.doc  3年B組.doc  3年D組.doc  4年B組.doc  5年A組.doc
1年B組.doc  1年D組.doc  3年A組.doc  3年C組.doc  4年A組.doc  4年C組.doc
```

## Q3 

2018年のすべての日付について、2,3,5,7が4つ含まれる日付を列挙してください（例: 2018年3月22日など）。

### 解答

```
$ dateutils.dseq 2018-01-01 2018-12-31 | tr -d - |
awk '{printf $0" ";print gsub(/[2357]/,"")}' | awk '$2==4'
```

## Q4

俳句を考え、次の短冊に縦書きで入れてください。

```
$ cat tanzaku
┏ ーー-┷-ーー┓
┃ 　　　　　 ┃
┃ 　　　　　 ┃
┃ 　　　　　 ┃
┃ 　　　　　 ┃
┃ 　　　　　 ┃
┃　　 　　　 ┃
┃　　 　　　 ┃
┗ーーーーーー┛
```

### 解答

俳句でないですが・・・

```
$ echo あついなつ　　 へんたいぜんら なつまつり　　 | xargs -n 1 | sed 's/./& /g' |
datamash transpose -t ' ' | sed '1i\ ' | paste <(cat tanzaku) - |
awk -F '' -v OFS='' 'NF<15;NF>14{$3=$15;$5=$13;$7=$11;$15=$13=$11="";print}'
┏ ーー-┷-ーー┓
┃ な　へ　あ ┃
┃ つ　ん　つ ┃
┃ ま　た　い ┃
┃ つ　い　な ┃
┃ り　ぜ　つ ┃
┃ 　　ん　　 ┃
┃ 　　ら　　 ┃
┗ーーーーーー┛
```

## Q5

`cowsay`の牛を右向きにして吹き出しの位置を調整して下さい。（万が一右向きオプションがあったら、それは使わずにお願いします。）

* 例

```
              ________________________________
             < あなたとJava今すぐダウンロード >
              --------------------------------
               ^__^   /
       _______/(oo)  /
   /\/(       /(__)
      | w----||
      ||     ||
```

### 解答

```
$ cowsay あなたとJava今すぐダウンロード |
awk '{printf $0;for(i=length;i<=30;i++)printf "@";print ""}' |
pee cat rev | awk 'NR<4||NR>11' | tr @ ' ' |
tr '\\' @ | tr '/' '\\' | tr @ / | tr '()' ')(' |
awk 'NR<4{printf "             "}{print}'
              ________________________________
             < あなたとJava今すぐダウンロード >
              --------------------------------
               ^__^   /
       _______/(oo)  /
   /\/(       /(__)
      | w----||
      ||     ||
```

## Q6

`seq 20`の出力について、次のように素数を丸囲みしてください。

```
1
②
③
4
⑤
6
⑦
8
9
10
⑪
12
⑬
14
15
16
⑰
18
⑲
20
```

### 解答

```
$ seq 20 | factor | awk 'NF==2{print $2}NF!=2{print $1}' |
mawk '!/:/{printf("&#x%x;\n",$1+"0x245f")}/:/' |
nkf --numchar-input | tr -d :
1
②
③
4
⑤
6
⑦
8
9
10
⑪
12
⑬
14
15
16
⑰
18
⑲
20
```

## Q7

`text`には、文字や空白、改行として認識されないバイナリが含まれています。どの行にどんなものがあるか調査してください。

### 解答

```
$ xxd -p text | tr -d '\n' | sed 's/e.....//g' | sed 's/0a/\n/g' | nl -ba
     1	00
     2
     3
     4
     5	02
     6
     7
     8	06
     9
    10	16
    11
    12
    13
    14
    15
    16
    17
```

## Q8


```
$ echo 嘘は嘘であると見抜ける人でないと（掲示板を使うのは）難しい
```

から始めて、出力で次のようにルビを打ってください。多少ずれたりスペースが入っても構いません。

```
ｳｿ  ｳｿ        ﾐﾇ      ﾋﾄ          ｹｲｼﾞﾊﾞﾝ  ﾂｶ        ﾑｽﾞｶ
嘘は嘘であると見抜ける人でないと（掲示板 を使うのは）難しい
```


### 解答

```
$ echo 嘘は嘘であると見抜ける人でないと（掲示板を使うのは）難しい |
mecab -E '' | awk -F"[\t,]" '{print $1,$(NF-1)}' | nkf -h |
sed -r 's/(.*) (.*)\1/\1 \2/' | awk 'NF==1{print $1,"*"}NF==2' |
datamash transpose -t ' ' | pee 'nkf --katakana | nkf -Z4' cat |
sed -n '2,3p' | column -t | sed 's/\([^ ]\)  /\1/g' | tr '*' ' '
ｳｿ  ｳｿ        ﾐﾇ      ﾋﾄ          ｹｲｼﾞﾊﾞﾝ  ﾂｶ        ﾑｽﾞｶ
嘘は嘘であると見抜ける人でないと（掲示板 を使うのは）難しい
```