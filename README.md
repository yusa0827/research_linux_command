# Linux Command 

# 実行環境
OS : Windows11, WSL2 


# 目標
1日1つはコマンドの使い方をまとめる  
コマンドは100個  


# 目次
1. #### [【date】日付や時刻を表示、設定する](#date)
2. #### [【sed】テキストの文字列を別の文字列に置換する](#sed)
3. #### [【tar】tar.gz の圧縮と解凍](#tar)
4. #### [【xargs】コマンドラインを作成して実行する](#xargs)
5. #### [【mv】ファイルやディレクトリを移動またはリネームする](#mv)
6. #### [【find】ディレクトリやファイルを見つける](#find)
7. #### [【ln】シンボリックリンクとハードリンクの作成方法](#ln)
8. #### [【factor】素因数分解する](#factor)
9. #### [【cd】ディレクトリを移動する](#cd)
10. #### [【ls】ファイルを一覧表示する](#ls)

# 例
1. #### [特定のフォルダから特定のテキストファイルを探し、特定の文字列の行を抽出したい](https://github.com/yusa0827/research_linux_command/example/find_xargs_cat_grep.md)


<a id="date"></a>

# 【date】日付や時刻を表示、設定する

さまざまな用途で利用する
* 現在の日時を取得  
* ファイルのタイムスタンプの設定  
* タイムスタンプによるシェルコマンドの操作


### 現在の日時を表示する
date  

日本標準時（JST）  

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ date
Sat Dec  2 23:12:20 JST 2023
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$
```

### UTCでの日付・時刻表示する
Universal time coordinated（協定世界時）  

出力結果にUTC と書かれている
```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ date -u
Sat Dec  2 14:13:57 UTC 2023
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$
```

### root権限で現在日時を設定する
sudo date -s "2023/12/25 00:00:00"
-s	システム時刻の設定  
管理者権限が必要  

### ファイルの更新日時(タイムスタンプ)を表示する
date -r file1.txt

-r ファイルパス  
ファイルの更新日時を表示  

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls -l file1.txt
-rwxrwxrwx 1 taso taso 8 Dec  2 21:19 file1.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ date -r file1.txt 
Sat Dec  2 21:19:46 JST 2023
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$
```

### ファイルの更新日時(タイムスタンプ)を変更する
touch コマンドを利用する

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls -l file1.txt
-rwxrwxrwx 1 taso taso 8 Dec  2 21:19 file1.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ touch -t 202312250101.01 file.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ touch -t 202312250101.01 file1.txt 
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls -l file1.txt
-rwxrwxrwx 1 taso taso 8 Dec 25  2023 file1.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$
```



### フォーマットを利用した日時表示
date +%F  
YYYY-MM-DD形式  

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ date +%F
2023-12-02
```


date +%T
hh:mm:ss

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ date +%T
23:20:57
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$
```



date "+%Y/%m/%d %H:%M:%S"
```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ date "+%Y/%m/%d %H:%M:%S"
2023/12/02 23:28:47
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ 
```


### 参考サイト
date コマンド  
https://hydrocul.github.io/wiki/commands/date.html  
【必見】dateコマンドの使い方｜フォーマットやオプションの一覧付  
https://itc.tokyo/linux/date-command/  
【Linux】dateコマンドで日付フォーマットの変更及び日付計算の方法　　
https://qiita.com/setonao/items/85435d5f7c480425ba95　　



<a id="sed"></a>

# 【sed】テキストの文字列を別の文字列に置換する
sed とは(stream editor)の略  
sed は、主にテキストにある文字列を別の文字列に置換する  


### 文字列を置換して出力する

sコマンドは正規表現で置換処理をする。

echo "ABC" | sed  "s/ABC/abc/g"  

3.3 The s Command  
Its basic concept is simple: the s command attempts to match the pattern space against the supplied regular expression regexp; if the match is successful, then that portion of the pattern space which was matched is replaced with replacement  
公式から引用　　


```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ echo "ABC"  
ABC
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ echo "ABC" | sed  "s/ABC/abc/"
abc
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$
```

オプション g はすべてのマッチした文字列を置換する。  
オプション g がないと、1行に2つ以上マッチした場合は1つ目しか置換されない。  

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ echo "ABC_ABC"
ABC_ABC
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ echo "ABC_ABC" | sed  "s/ABC/abc/"
abc_ABC
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ echo "ABC_ABC" | sed  "s/ABC/abc/g"
abc_abc
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$
```

### 参考サイト
sed, a stream editor  
https://www.gnu.org/software/sed/manual/sed.html#sed-script-overview  

### 複数の文字列を置換して出力する
echo "ABC_DEF" | sed -e "s/ABC/abc/" -e "s/DEF/def/g"  
オプション -e を使うと複数で条件指定が可能  


```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ echo "ABC_DEF" | sed -e "s/ABC/abc/" -e "s/DEF/def/g"
abc_def
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$
```

### テキストの文字列を置換してテキストに出力する

1. パイプラインの方法  
cat file1.txt | sed -e "s/ABC/abc/g" > file1_output.txt  

オプション -e コマンドを複数実行することができる  

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls
file1.txt  file2.txt  file3.txt  folder1  folder1.tar.gz  folder2  folder3  folder4  tmp
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ echo "ABC_ABC" > file1.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cat file1.txt
ABC_ABC
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cat file1.txt | sed -e "s/ABC/abc/g" > file1_output.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cat file1_output.txt
abc_abc
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ 
```

2. sed コマンドの方法 別のテキストに出力する  
sed -e "s/ABC/abc/g" file1.txt > file1_output2.txt  

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ sed -e "s/ABC/abc/g" file1.txt > file1_output2.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cat file1.txt
ABC_ABC
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ sed -e "s/ABC/abc/g" file1.txt > file1_output2.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cat file1_output2.txt
abc_abc
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ 
```

3. sed コマンドの方法 上書きする
sed -i "s/ABC/abc/g" file1.txt  
-i, --in-place  
標準出力せずにファイルを上書き  

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cat file1.txt 
ABC_ABC
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ sed -i "s/ABC/abc/g" file1.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cat file1.txt 
abc_abc
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$
```


### 参考サイト
sedコマンド基本  
https://qiita.com/shunbaba/items/faf0cf2dbfd4e205e945  
sed コマンド
https://hydrocul.github.io/wiki/commands/sed.html


### タブ文字を全置換する
sed '/\t/ /g'  


### 空行を削除する
^$ という正規表現と 削除コマンドd を組み合わせる  

cat file | sed '/^$/d'  


### 参考サイト
sed, a stream editor  
https://www.gnu.org/software/sed/manual/sed.html#sed-script-overview  
sed コマンド  
https://hydrocul.github.io/wiki/commands/sed.html  


### 参考サイト
sedコマンド基本  
https://qiita.com/shunbaba/items/faf0cf2dbfd4e205e945




<a id="tar"></a>

# 【tar】tar.gz の圧縮と解凍

### tar.gz の圧縮
tar -zcvf folder1.tar.gz folder1  

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ tar -zcvf folder1.tar.gz folder1
folder1/
folder1/file1.txt
folder1/file2.txt
folder1/file3.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls
file1.txt  file2.txt  file3.txt  folder1  folder1.tar.gz  folder2  folder3  folder4  tmp
```

### tar.gz の解凍
tar -zxvf folder1.tar.gz  
folder1.tar.gz ファイルで圧縮される前のファイル・フォルダの状態のまま、解凍される

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ tar -zxvf folder1.tar.gz 
folder1/
folder1/file1.txt
folder1/file2.txt
folder1/file3.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ 
```


### 参考サイト
[Linux]ファイルの圧縮、解凍方法  
https://qiita.com/supersaiakujin/items/c6b54e9add21d375161f  


<a id="xargs"></a>

# 【xargs】コマンドラインを作成して実行する
使いこなせたら、かっこいい

### 特定のファイル・フォルダを見つけて、削除する

find file* | xargs rm -v  
rm, -v, --verbose         explain what is being done  

fileがつくファイル・フォルダを見つけて、  
それらを削除する  

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls
file1.txt  file2.txt  file3.txt  folder1  folder2  folder3  folder4
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ find "file*"
find: ‘file*’: No such file or directory
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ find file* 
file1.txt
file2.txt
file3.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ find file* | xargs rm -v
removed 'file1.txt'
removed 'file2.txt'
removed 'file3.txt'
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls
folder1  folder2  folder3  folder4
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$
```

### 特定のファイル・フォルダを見つけて、削除することをドライランする
file file* | xargs -p rm -v  
-p, --interactive            prompt before running commands  

ドライラン：予行演習、空運転、リハーサルなどの意味  

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls
file1.txt  file2.txt  file3.txt  folder1  folder2  folder3  folder4
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ file file*
file1.txt: empty
file2.txt: empty
file3.txt: empty
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ file file* | xargs -p rm -v
rm -v file1.txt: empty file2.txt: empty file3.txt: empty ?...
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$
```


### 特定のファイル・フォルダを見つけて、コピーする

find file* | xargs -i cp {} tmp/　　
-i, --replace[=R]            replace R in INITIAL-ARGS with names read　　
                                 from standard input; if R is unspecified,　　
                                 assume {}　　
オプション -i は、 {} で　引数の位置を指定する


```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls
file1.txt  file2.txt  file3.txt  folder1  folder2  folder3  folder4  tmp
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls tmp/
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ find file*
file1.txt
file2.txt
file3.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ find file* | xargs -p -i cp {} tmp/
cp file1.txt tmp/ ?...
cp file2.txt tmp/ ?...
cp file3.txt tmp/ ?...
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ find file* | xargs-i cp {} tmp/
xargs-i: command not found
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ find file* | xargs -i cp {} tmp/
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls tmp/
file1.txt  file2.txt  file3.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$
```


### 特定のファイル・フォルダを見つけて、複数プロセスで同時にコピーする
find file* | xargs -i -P 4 cp {}   
  -P, --max-procs=MAX-PROCS    run at most MAX-PROCS processes at a time  
オプション -P で複数のプロセスを同時に立ち上げて実行  

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls
file1.txt  file2.txt  file3.txt  folder1  folder2  folder3  folder4  tmp
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls tmp/
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls
file1.txt  file2.txt  file3.txt  folder1  folder2  folder3  folder4  tmp
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ find file* | xargs -p -i -P 4 cp {} tmp/        
cp file1.txt tmp/ ?...
cp file2.txt tmp/ ?...
cp file3.txt tmp/ ?...
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls tmp/
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ find file* | xargs -i -P 4 cp {} tmp/
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls tmp/
file1.txt  file2.txt  file3.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$
```


### テキストに書かれたファイル名をテキストファイルとして作成する
cat file1.txt | xargs touch　　

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ echo  test_file.txt > file1.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cat file1.txt
test_file.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cat file1.txt | xargs touch
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls
file1.txt  file2.txt  file3.txt  folder1  folder2  folder3  folder4  tmp
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls
file1.txt  file2.txt  file3.txt  folder1  folder2  folder3  folder4  test_file.txt  tmp
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls
file1.txt  file2.txt  file3.txt  folder1  folder2  folder3  folder4  test_file.txt  tmp
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$
```


### 参考サイト
xargs コマンドとは  
https://tech-lab.sios.jp/archives/29544  
【Linux】xargsコマンドの使い方　　
https://qiita.com/P-man_Brown/items/c3f2634b7b5e08306c8f  
xargsコマンドで覚えておきたい使い方・組み合わせ7個(+1個)　　
https://orebibou.com/ja/home/201507/20150727_001/  
【必読】便利なxargsコマンドの使い方を実例付きで丁寧に解説
https://itc.tokyo/linux/xargs-command/


<a id="mv"></a>

# 【mv】ファイルやディレクトリを移動またはリネームする


「mv」は、下記の①と②ができる。  
①ファイルやディレクトリを移動
②リネームしたりするコマンドです。

### ファイルを移動する
mv [src] [dst]

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls
folder1  folder2  folder3
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ mv folder1/file1.txt file1.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls
file1.txt  folder1  folder2  folder3
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$
```


### ファイルをリネームする
mv [file_a] [file_b] 

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls
file1.txt  folder1  folder2  folder3
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ mv file1.txt file2.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls
file2.txt  folder1  folder2  folder3
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$
```


### 複数のファイルを1つのディレクトリに移動する
mv [file_a] [file_b] [file_c] [folder] 

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls
file1.txt  file2.txt  file3.txt  folder1  folder2  folder3  folder4
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ mv file1.txt file2.txt file3.txt folder4
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls folder4/
file1.txt  file2.txt  file3.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$
```


### 移動した先に同名ファイルがあれば上書きする
mv -f file1.txt folder1/file1.txt  
-f, --force

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls
file1.txt  file2.txt  file3.txt  folder1  folder2  folder3  folder4
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cat file1.txt
test1
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cat file1.txt
test1
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cat folder1/file1.txt 
test
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ mv -f file1.txt folder1/file1.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cat file1.tx
cat: file1.tx: No such file or directory
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cat file1.txt
cat: file1.txt: No such file or directory
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cat folder1/file1.txt
test1
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ 
```



### 移動した先に同名ファイルがあれば上書きするかを確認する
mv -i file1.txt file2.txt　　
-i, --interactive  

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls
file1.txt  file2.txt  file3.txt  folder1  folder2  folder3  folder4
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ mv -i file1.txt file2.txt
mv: overwrite 'file2.txt'? y
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls
file2.txt  file3.txt  folder1  folder2  folder3  folder4
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$
```



### 移動した先に同名ファイルがあれば上書きしない、移動もしない

mv -n file1.txt folder1/file1.txt  
-n, --no-clobber


```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ echo test2 > folder1/file1.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cat file1.txt
test1
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cat folder1/file1.txt
test2
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ mv -n file1.txt folder1/file1.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls
file1.txt  file2.txt  file3.txt  folder1  folder2  folder3  folder4
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cat folder1/file1.txt
test2
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ 
```



### 上書きされるファイルをバックアップする
mv -b file1.txt file1.txt  
-b, --backup  

バックアップされたファイル名は、最後に"~" が付く  
```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cat file1.txt
test1
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cat file2.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ mv -b file1.txt file1.txt
mv: 'file1.txt' and 'file1.txt' are the same file
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ mv -b file1.txt file2.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ ls
file2.txt  file2.txt~  file3.txt  folder1  folder2  folder3  folder4
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cat file2.txt
test1
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cat file2.txt~
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ 
```


### 参考サイト 
【 mv 】コマンド――ファイルやディレクトリを移動する／名前を変更する  
https://atmarkit.itmedia.co.jp/ait/articles/1606/13/news024.html  
【Linuxコマンド】mvでファイル・ディレクトリを移動する方法
https://www.sejuku.net/blog/49611


<a id="find"></a>

#  【find】ディレクトリやファイルを見つける


find コマンドは、検索するためのコマンドです。　　
ファイルやディレクトリを検索する際に用います。　　


### ディレクトリのみを対象に検索する

find -type d  
ディレクトリを対象に検索  

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ find -type d
.
./folder1
./folder2
./folder3
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ 
```

### ファイルのみを対象に検索する

find -type f  
ファイルのみを対象に検索  

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ find -type f
./folder1/file1.txt
./folder1/file2.txt
./folder1/file3.txt
./folder2/file1.txt
./folder2/file2.txt
./folder2/file3.txt
./folder3/file1.txt
./folder3/file2.txt
./folder3/file3.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$
```


### 特定の文文字列のみを対象に検索する

find  -name [file]

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ find  -name file1.txt
./folder1/file1.txt
./folder2/file1.txt
./folder3/file1.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ 
```

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ find -type d -name folder1
./folder1
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ 
```

### 複数条件(-and, -or, -not) で 条件に当てはまるファイルやディレクトリを検索する


```

```


### 参考サイト
find コマンド 【使い方 まとめ】  
https://tech-blog.rakus.co.jp/entry/20220831/find  
ファイルなどを検索する！findコマンドの詳細まとめ【Linuxコマンド集】  
https://eng-entrance.com/linux-command-find  


<a id="ln"></a>

# 【ln】シンボリックリンクとハードリンクの作成方法</a>

### シンボリックリンクとは  
Windows だとショートカットのことです。  
本体であるファイルやディレクトリが位置する場所とは別に、その本体に対する別名のリンクを別の場所に作成するためにシンボリックリンクを使います。  
コピーを作成するのではない。    
例えばある場所に配置されたファイルを、あたかも別の場所に存在するかのように扱うことができます。


### ハードリンクの作成
ln <file> <hard_link>

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test/folder1$ ls
file1.txt  file2.txt  file3.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test/folder1$ ln file1.txt  f
ile1_txt_hard_link
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test/folder1$ ls
file1.txt  file1_txt_hard_link  file2.txt  file3.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test/folder1$ ls -l
total 0
-rwxrwxrwx 2 taso taso 3 Nov 29 23:45 file1.txt
-rwxrwxrwx 2 taso taso 3 Nov 29 23:45 file1_txt_hard_link
-rwxrwxrwx 1 taso taso 0 Nov 28 23:23 file2.txt
-rwxrwxrwx 1 taso taso 0 Nov 28 23:23 file3.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test/folder1$
```


### ハードリングとは  
Linux(Unix) だとすべてのファイルは、inode と呼ばれるファイルシステム上で一意のデータを参照します。
ディスク上の実体のデータに対して一意な inode が存在し、それをファイル名でリンクされているイメージです。  
inode に対して必ず1つ以上の ハードリンク が存在します。  
つまり作成されたファイルやディレクトリは1つの inode とハードリンクでつながります。  
ハードリンクを別途作成する場合、1つの inode に対して複数のハードリンクで参照するファイルやディレクトリが存在するようになります。  

一つのファイルに対し，複数の実名を付ける処理がハードリンクである。ハードリンクの場合，複数あるファイル名はどれも対等なものとなる。  


### シンボリックリンクの作成
ln -s <file> <symbolic_link>

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test/folder1$ ln -s file1.txt file1_txt_symbolic_link
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test/folder1$ ls
file1.txt  file1_txt_symbolic_link  file2.txt  file3.txt
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test/folder1$ ls -li
total 0
 8725724278589409 -rwxrwxrwx 1 taso taso 0 Nov 28 23:23 file1.txt
15481123719280442 lrwxrwxrwx 1 taso taso 9 Nov 29 23:43 file1_txt_symbolic_link -> file1.txt        
 1970324837533668 -rwxrwxrwx 1 taso taso 0 Nov 28 23:23 file2.txt
 1407374884112357 -rwxrwxrwx 1 taso taso 0 Nov 28 23:23 file3.txt
```


### 参考サイト
[Linux] ln シンボリックリンクとハードリンクの違いと作り方  
https://webbibouroku.com/Blog/Article/linux-ln  
シンボリックリンクとハードリンクの違い  
https://qiita.com/katsuo5/items/fc57eaa9330d318ee342


<a id="factor"> </a>

# 【factor】素因数分解する
factor <number>  

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command$ factor 123
123: 3 41
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command$ factor 123123412
123123412: 2 2 30780853
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command$ factor 30780853
30780853: 30780853
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command$
```

<a id="cd"></a>

# 【cd】ディレクトリを移動する
cd コマンド  

cdコマンドの「cd」は、「change directory」の略です。  


### 指定したディレクトリに移動
cd <folder>

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cd folder1
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test/folder1$ 

```

### １つ上の階層のディレクトリに移動
cd ..


```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test/folder1$ cd ..
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ 
```


### ホームディレクトリ以下に移動
cd と cd ~ は同じ結果  

cd  

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cd 
taso@LAPTOP-4VD8MIEJ:~$
```

cd ~  

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cd ~
taso@LAPTOP-4VD8MIEJ:~$ 
```


### 1つ前にいたディレクトリに移動する
cd -

```
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$ cd folder1  
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test/folder1$ cd -
/mnt/c/Users/sasak/Desktop/research_linux_command/test
taso@LAPTOP-4VD8MIEJ:/mnt/c/Users/sasak/Desktop/research_linux_command/test$
```

### シンボリックへの移動
cd [オプション] [ディレクトリ]  
  
-P	シンボリックリンクの場合、シンボリックリンクのターゲットに移動します。  
-L	シンボリックリンクの場合、シンボリックリンクに移動します。  



### 参考サイト 
【cd】Linuxでディレクトリを移動するコマンド
https://uxmilk.jp/27431

Linuxコマンド【 cd 】作業ディレクトリを移動する  
https://webkaru.net/linux/cd-command/  

<a id="ls"></a>

# 【ls】ファイルを一覧表示する </a>
ls コマンド

lsコマンドは「list segments」　　
ディレクトリやファイルを表示するためのコマンドです。　　

### 作業ディレクトリのファイルやフォルダを表示する

```
$ ls
folder1  folder2  folder3
$

```


### 作業ディレクトリのファイルやフォルダを1列で表示する

ls -1  

```
$ ls -1       
folder1
folder2
folder3
$
```

### 作業ディレクトリのファイルやフォルダを再帰的にリストアップする

ls -R  

```
$ ls -R
.:
folder1  folder2  folder3

./folder1:
file1.txt  file2.txt  file3.txt

./folder2:
file1.txt  file2.txt  file3.txt

./folder3:
file1.txt  file2.txt  file3.txt
$
```

### 作業ディレクトリのファイルやフォルダをロングフォーマットでリストアップする

ls -l  
  
下記を表示  
コンテンツのパーミッション  
ハードリンク数  
所有者  
所有グループ  
バイトで表したサイズ  
コンテンツの最終変更日／時間  
ファイルまたはディレクトリの名前  

```
$ ls -l
total 0
drwxrwxrwx 1 taso taso 512 Nov 28 23:23 folder1
drwxrwxrwx 1 taso taso 512 Nov 28 23:23 folder2
drwxrwxrwx 1 taso taso 512 Nov 28 23:23 folder3
$
```

### 作業ディレクトリのファイルやフォルダをリストアップし日付と時間でソートして表示

ls -t   
  
folder1, folder2, folder3 の順番に作成したので、  
時間でソートされている  

```
$ ls -t       
folder3  folder2  folder1
```

### 作業ディレクトリのファイルやフォルダをリストアップしファイルサイズでソートして表示

ls -S

```
$ ls -S
folder1  folder2  folder3
```


### 特定のディレクトリの中身を表示

ls <folder>

```
$ ls folder1  
file1.txt  file2.txt  file3.txt
$
```


### lsの主なオプション

```
オプション	説明
-a	先頭にピリオドがあるファイル（隠しファイル）を表示する
-l	一覧化して詳細を表示する
-h	読みやすい形式で表示する
-1	縦に並べて表示する
-t	更新日付順に表示する
-X	ファイルの拡張子別に表示する
-p	ディレクトリは「/」をつけて表示する
-m	ファイルを,（カンマ）で区切って表示する
```


### 参考サイト ls コマンド
Linux の LS コマンドについて – ディレクトリの中のファイルをリストアップする方法 + オプションフラグ  
https://www.freecodecamp.org/japanese/news/the-linux-ls-command-how-to-list-files-in-a-directory-with-options/  


