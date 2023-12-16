# 特定のフォルダから特定のテキストファイルを探し、特定の文字列の行を抽出したい


"特定のフォルダから特定のテキストファイルを探し" は find コマンドを使用する

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls
file.txt  file1.txt  file1_output.txt  file1_output2.txt  file2.txt  file3.txt  folder1  folder1.tar.gz  folder2  folder3  folder4  tmp
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls folder1
file1.txt  file2.txt  file3.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ find folder1/ -type f -name "file1.txt"
folder1/file1.txt
```

"特定の文字列の行を抽出したい"は、find コマンドで出力したファイルを、xargs コマンドを使って cat コマンドの引数として渡し、表示させる

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ find folder1/ -type f -name "file1.txt" | xargs cat

#incldue <boost/test1>

#incldue <boost/test2>

#incldue <boost/test3>
```

"特定の文字列の行を抽出したい"は、grepコマンドを使用する

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ find folder1/ -type f -name "file1.txt" | xargs cat | grep boost
#incldue <boost/test1>
#incldue <boost/test2>
#incldue <boost/test3>
```

### ホームに戻る
[# Linux Command ](https://github.com/yusa0827/research_linux_command)
