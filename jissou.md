##実装メモ
最初に
'sudo apt-get install clang-8 lldb-8 lld-8'
としたが、
' /bin/sh:1 clang++: not found '
とエラーが出た。
そこで、
' sudo apt-get install clang'
とすると解決した。
その後はcloneしてmakeして開発開始。
