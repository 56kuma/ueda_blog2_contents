---
Keywords: うんこ,シェル芸,割とどうでもいい
Copyright: (C) 2017 Ryuichi Ueda
---

# うんこシェル芸ドリル

* 諸注意
  * 解答はMacの端末でUbuntu 16.04にSSH接続して作りました。
  * 必要なコマンドは各自インストールのこと。
  * うんこ漢字ドリルではない。


## 💩1

lsをunkoと打ち間違える癖に悩んでいる方も多いと思います。そこで矯正のため、次のようにlsをunkoと打ち間違えると、端末の幅いっぱいにうんこメッセージをスクロールさせるエイリアスを設定してください。

![恥ずかしいgifアニメ](unko_q1.gif)

### 解答

* https://gist.github.com/Iruyan-Zak/186ce5d5cf8164744721dbf2f9326ef1


```bash
$ alias unko='echo -ne "@@unko@@yes" | perl -pe "\$_ x= 20" | head -c $(tput cols) | sed "s/@/💩/g" | sed -E ":b;p;s/(.)(.*)/\2\1/;bb" | xargs -i bash -c "sleep 0.2 && echo -ne \\\\r{}"'
```

## 💩2

次のように楽しげに💩を回してください。

<img width="400" src="unko_q2.gif" >

### 解答例

```bash
$ while sleep 0.02 ; do clear ; echo 💩  $(date +%N) | awk '{t=2*3.14*$2/1000000000;c=cos(t)*5+5;s=sin(t)*10+13;for(i=1;i<=c;i++)print "";for(j=1;j<=s;j++)printf " ";print $1}'; done
```

## 💩3

次の文を「う」「ん」「こ」「ー」のみでエンコードして、デコードしてください。

```
2017年はうんこの年でした。うんこうんこ氏のうんこの党がうんこアウフヘーベン発言で頓挫しました。
```

### 解答

* エンコード

```bash
$ echo 2017年はうんこの年でした。うんこうんこ氏のうんこの党がうんこアウフヘーベン発言で頓挫しました。|
xxd -b | awk '{$1="";$NF="";print}' | tr -d ' ' | sed 's/../ &/g' |
sed -e 's/ 00/う/g' -e 's/ 01/ん/g' -e 's/ 10/こ/g' -e 's/ 11/ー/g' > unko_yuriko
$ cat unko_yuriko 
うーうこうーうううーうんうーんーーこんんこーこん
こーんうーこうーこううんここーーーこうーこううん
こうんこーこうーこううここんうーーこうーこううん
こんうーーこうーこううんここーこーこんんこーこん
こーんうーこうーこううんここんーーこうーこううん
こんんーーこうーこううんこんーーーこうーこううう
こううこーこうーこううんこうんこーこうーこううこ
こんうーーこうーこううんこんうーーこうーこううん
こうんこーこうーこううここんうーーこうーこううん
こんうーーこんここーううこうーーーこうーこううん
ここーこーこうーこううんこうんこーこうーこううこ
こんうーーこうーこううんこんうーーこうーこううん
ここーこーこんんこうんんこんここーこうーこううん
こうーうーこうーこううんこうんこーこうーこううこ
こんうーーこうーこううんこんうーーこうーこううこ
ここうこーこうーこううこここんこーこうーこううー
こんんんーこうーこううーこんこうーこうーこううー
こーーうーこうーこううーこんこんーこうーこううー
こーうーーこんーこんこんこーここーここうこここう
こうううーこうーこううんここんーーここんここうう
こんうーーこんここうーうこここーーこうーこううん
こんんーーこうーこううんこーーこーこうーこううん
こんんーーこうーこううんこんーーーこうーこううう
こううこううここ
```

* デコード

```bash
$ cat unko_yuriko | sed -e 's/う/0 /g' -e 's/ん/1 /g' -e 's/こ/2 /g' -e 's/ー/3 /g' | xargs -n 2 | awk '{print $1*4 + $2}' | xargs printf "%x" | xxd -p -r
2017年はうんこの年でした。うんこうんこ氏のうんこの党がうんこアウフヘーベン発言で頓挫しました。
```

## 💩3

`/dev/urandom`の出力から小文字大文字のアルファベットだけを残し、その中に流れるunkoの平均流速を概算しなさい。なお、大文字小文字は区別しない。

* 例

次のように26文字に一つ「unko」とある場合は、38[unko/kb]となる。

```
$ echo abadojfwejaiefUnkofawfewaf | awk '{print 1/length($0)}'
0.0384615
```

### 解答

```bash
$ cat /dev/urandom | tr -dc 'A-Za-z' | tr a '\n' |
tee /tmp/unko | grep -oi -m 100 unko &&
wc -c /tmp/unko | awk '{print $1/(100*1000*1000)"[unko/MB]"}'
UNko
UnKO
UnKo
unKO
Unko
UNKO
UnKo
UNKO
UNKo
unKo
uNKo
unKO
Unko
unko
UnKo
uNko
UNKO
UNko
UnKO
Unko
Unko
UNKO
uNKo
Unko
uNKO
unKO
UnKO
UNKo
unko
uNkO
uNKO
unKo
unKo
unkO
UNkO
UnKo
uNko
uNKO
unko
unKO
unKO
UNKO
unKO
unko
unKo
uNko
UNKO
UNko
uNkO
uNko
UnkO
UnKo
UnKo
uNko
UNKO
uNKO
unko
unKo
uNko
uNkO
UnKo
UNko
UNkO
UNKo
uNkO
UnKo
UnkO
UNko
UNKO
UnkO
unko
unKO
unko
UNkO
Unko
unkO
unkO
unKo
unKo
UNko
unKO
UnKo
uNKO
UNko
unKo
UnKO
uNKO
UNKo
UnKO
UNKo
uNKO
unKo
UNKO
UNko
UNko
UnkO
UNKO
unKO
UnKO
UNko
0.48599[unko/MB]
```

ということで、0.5ウンコパーメガバイトだと分かる。

## 💩8 

これを電車の中で人に見られながら作成していた筆者の心境を説明せよ。