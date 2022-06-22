# CASL2 アセンブラ/ COMET2 エミュレータ for KIT 言語処理プログラミング

CASL2, COMET2のJavaScript実装です．
オリジナルのperl版は https://github.com/omzn/casl2 

## 開発中

方針: 1枚もののオフラインWebページで実行可能にする．

### casl2.js

* 状況: ほぼ完成

以下で実行できます．
```
$ node casl2.js hoge.cas
```
Webページから呼ぶ際はmain()を呼べばOK．
配列 comet2mem に機械語が格納される．

### comet2.js

* 状況: 50%
  * 入出力のやりとりがない関数群は移植済み．
  * 入出力をどうするか．
    * 暫定的にSTDINを`input`要素, STDERR, STDOUTを`textarea`要素に対応づけてしまうか…？
    * コマンドラインから実行できるように, node.js仕様にしてしまうか．

### 独自拡張

* ラベルにはスコープがあります．スコープはプログラム内(START命令からEND命令で囲まれた部分)のみです．
* CALL命令にもスコープが効きますが，CALLだけは別プログラムの開始ラベル(START命令のラベル)まで参照することができます．
* 簡単のため，MULA (算術乗算), MULL (論理乗算), DIVA (算術除算), DIVL (論理除算)を実装しています．利用方法はADDA, ADDL等とほぼ同じです．
  * DIVA, DIVLについては，0除算を行おうとするとZFとOFが同時に立って，計算は行われずに先に進みます．


