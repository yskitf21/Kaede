### 2023/3/4

* * *

-   成果
    -   関数呼び出しが成功するようになった

-   while文の修正
    -   1ループごとにスタックの深さが1ずつ増えてしまっていたので1ループごとにpop raxした

-   関数呼び出しの修正
    -   「call命令の際にレジスタの倍数が16の倍数になっていなければならない」という問題があった
    -   codegen.cにstack_depthという変数を用意して、depthが偶数のときにのみcall命令の前にpushを行ってrspを8ズラした
    -   ↑本来は「奇数のときに」pushを行うべきなのになぜか逆にしたら動いた。

* * *

### 2023/3/9

* * *

-   codegenの修正が完了
    -   codegen.cにgen_stmtを生やして、main.cでの無条件のpop raxをやめた。
    -   これに伴い,elseがないときに無条件で右の子にND_NUMをくっつける必要がなくなったため,parse.cの該当部分を削除。code_genのif部分で右の子があるときだけelseの処理をするように修正。
-   関数定義の実装（引数無し、parseが完了）
    -   新しいparse用の関数functionを追加。
    -   もとのND_FUNCをND_FUNC_CALLに改名し、さらにND_FUNC_DEFを追加。

* * *

### 2023/3/14

* * *

-   main関数がITF関数になった

-   main.cでやっていたプロローグとエピローグを消した
    -   main.cで "main:"のアセンブリを吐かないようにした
    -   その代わり、関数定義でITF関数がやってきたときだけ"main:"のアセンブリを吐くようにした

-   関数ごとにローカル変数を定義するようにした

-   プログラムの一番外のネストには「関数定義」または「変数の宣言・定義」の2種類以外を認めない、というルールを設けることにした

-   引数なしの関数定義実装完了


-   次回以降
    -   関数に引数を入れる
    -   インクリメントほしい（ゆーすけ）
    -   \+=,-=,\*=,/=ほしい (kerusu)

* * *