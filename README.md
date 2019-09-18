### ミニキャン言語(MC)講義　第一回事前課題

第一回事前課題では、数字と二項演算子のみからなるexpressionをコンパイルし、オブジェクトファイルを得ることが目標です。第一回の課題は全部で6つあります。分からないことがあったらkintoneでどんどん質問をして下さい。また、他の参加者の質問で答えられるものがあれば是非積極的に答え、助け合って下さい。

#### 1.1 コンパイラについての文献を読む

参加者の皆様の中にはあまりプログラミング経験の無い方からコンパイラやインタプリタを自作した事がある方まで幅広い技術背景を持った方がいると思うので、まずは基礎知識の土台を作るためにいくつか参考文献を紹介します。

[植山類さんによるコンパイラ作成入門](https://www.sigbus.info/compilerbook)は基礎的な内容から始まり丁寧にコンパイラの作り方が解説してあり、「ASTと聞いてピンとこない」方は読むと非常に勉強になると思います。[LLVM Kaleidoscope](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/index.html)は私がこの講義をデザインする際に非常に参考にさせて頂いた、LLVM backendで言語を作る際のチュートリアルです。英語ですが、講義では触れられない最適化についてのセクションもあるので余力がある方は見てみて下さい。

#### 1.2 環境構築

LLVM/Clangをインストールし、このgithubリポジトリを手元にcloneし、makeをして下さい。ソースコード中に解説をコメントとして沢山書いたつもりなので、目を通すと全体像が掴めると思います。

makeをすると、`mc`という実行可能ファイルが出来ます。これがMC言語のコンパイラになります。`./mc test/test1.mc`とコンパイルすると、エラーは出ますが`output.o`というオブジェクトファイルが出来ます。今はこのオブジェクトファイルは空っぽですが、1.7までの課題を終えるとちゃんと意味のある中身が入るオブジェクトファイルになります。mc言語でサポートする型は64bit整数型のみのため、今回は`1+4;`, `(4+2)*300+(5-3)`等の数字と二項演算子のみからなるexpressionをコンパイルし、オブジェクトファイルにすることが目標です。test/ディレクトリにいくつかテストと期待されるアウトプットが置いてあり、課題を進めていく度に実装が正しいか確認することが出来るようになっています。

主に使うのはsrc/の中の`codegen.h`, `lexer.h`, `parser.h`というファイルです。`mc.cpp`は`main`がある呼び出し元で、それらをincludeしています。`helper/helper.h`はオブジェクトファイルを作るための補助的なファイルで、あまり気にしなくて大丈夫です。

#### 1.3 数字のトークナイザを実装してみよう

以降の課題は実際にソースコードを書く課題になります。少し難しそうに見えるかもしれませんが、コメントに誘導を付けたので心配しなくても大丈夫です。

`lexer.h`の中で`TODO 1.3`とコメントアウトがしてある箇所があるのでそこを探して下さい。コメントに実装の方針が書いてあるので、それを参考に数字をトークナイズするコードを書いて下さい。

この課題が解き終わると、`test/test1.mc`が正常にコンパイル出来るようになるはずです。期待される出力は`test/test1_expected_output.txt`にあります。

#### 1.4 コメントアウトを実装してみよう

`lexer.h`の中で`TODO 1.4`とコメントアウトがしてある箇所があるのでそこを探して下さい。コメントに実装の方針が書いてあるので、それを参考に`#`から始まる行をコメントとして無視するコードを書いて下さい。

この課題まで解き終わると、`test/test2.mc`が正常にコンパイル出来るようになるはずです。

#### 1.5 括弧を実装してみよう

`parser.h`の中で`TODO 1.5`とコメントアウトがしてある箇所があるのでそこを探して下さい。コメントを参考に、括弧をパースするコードを書いて下さい。

この課題まで解き終わると、`test/test3.mc`が正常にコンパイル出来るようになるはずです。

#### 1.6 二項演算のパーシングを実装してみよう

このセクションが今回の課題の中で一番難しいかもしれません。`parser.h`の中で`TODO 1.6`とコメントアウトがしてある箇所があるので探して下さい。実装の方針を参考に、`+`, `-`, `*`と数値からなる二項演算をパーシングするコードを書いて下さい。

この課題まで解き終わると、`test/test4`が正常にコンパイル出来るようになるはずです。

#### 1.7 `-`と`*`に対してIRを作ってみよう

`codegen.h`の中で`TODO 1.7`のコメントを探して下さい。この課題はとても簡単で、`+`に対するコードはあるので、それとほぼ同じことをします。

この課題まで解き終わると、`test/test5.mc`が正常にコンパイル出来るようになるはずです。


課題は以上になります。お疲れ様でした！！

#### 実装メモ
最初に
`sudo apt-get install clang-8 lldb-8 lld-8`としたが、

`/bin/sh:1 clang++: not found `とエラーが出た。

そこで、
`sudo apt-get install clang`
とすると解決した。

その後はcloneしてmakeして開発開始。

