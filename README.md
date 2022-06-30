# CASL2 アセンブラ/ COMET2 エミュレータ for KIT 言語処理プログラミング

CASL2, COMET2のJavaScript実装です．
オリジナルのperl版は https://github.com/omzn/casl2 

## 開発中

方針: 1枚もののオフラインWebページで実行可能にする．

* test.html に必要なものがすべて書いてある．

### casl2.js

* 状況: ほぼ完成

コマンドラインからは以下で実行できます．
```
$ node casl2.js hoge.cas
```
配列 comet2ops にアセンブル後の機械語が格納され， comet2実行時に comet2mem にコピーされる．

### comet2.js

* 状況: 50%
  * 入出力のやりとりがない関数群は移植済み．
  * terminal.jsを利用して，Webページ上の簡易ターミナルで動かすようにした． そのため，インタラクティブインターフェイスがそのまま利用できる．

* TODO:
  * 出力を標準入出力にもできるように実装する．(node.jsでの実行もサポート)
  * シミュレータで動かしているプログラムで無限ループが発生する場合，それを安全に止める方法が必要になる．
    * 具体的には，runコマンドでの実行で意図的に無限ループとなる場合．
    * `run_stop`を1にすれば止まる．
  * `cmd_hoge`の関数群を実装する．
  * `exec_in`, `exec_out`を実装する．

### 独自拡張

* ラベルにはスコープがあります．スコープはプログラム内(START命令からEND命令で囲まれた部分)のみです．
* CALL命令にもスコープが効きますが，CALLだけは別プログラムの開始ラベル(START命令のラベル)まで参照することができます．
* 簡単のため，MULA (算術乗算), MULL (論理乗算), DIVA (算術除算), DIVL (論理除算)を実装しています．利用方法はADDA, ADDL等とほぼ同じです．
  * DIVA, DIVLについては，0除算を行おうとするとZFとOFが同時に立って，計算は行われずに先に進みます．


