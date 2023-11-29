# Linux Command 

# 実行環境
OS : Windows11, WSL2 


# 素因数分解する
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


# ディレクトリを移動する
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

# ファイルを一覧表示する
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


