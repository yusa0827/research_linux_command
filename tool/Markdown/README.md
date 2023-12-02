# Markdown 記法


# 【#】見出し


# 見出し1
## 見出し2
### 見出し3
#### 見出し4
##### 見出し5
###### 見出し6  
####### 見出し7  
シャープの数は 6まで    



```
# 見出し1
## 見出し2
### 見出し3
#### 見出し4
##### 見出し5
###### 見出し6  
####### 見出し7
```

# 【``】CODE記法
バッククォートで文字列を囲むこと

ファイルのコピーのコマンドは、`cp src dst` である  

```
ファイルのコピーのコマンドは、`cp src dst`である
```

### 参考サイト
Markdown記法 サンプル集  
https://qiita.com/tbpgr/items/989c6badefff69377da7  


# 【** **】文字を強調  
「 *（アスタリスク）」で囲むことで強調 　　


文字を**強調**する  

```
文字を**強調**する 
```

文字を***強調***する  

```
文字を***強調***する
```

### 参考サイト
Markdown記法 サンプル集  
https://qiita.com/tbpgr/items/989c6badefff69377da7  


# 【ul】箇条書きリスト

「番号なしリスト（箇条書きリスト）」　　
番号なしリストは、*（アスタリスク）、+（プラス）、-（ハイフン）を使用　　


* A
* B
* C

```
* A
* B
* C
```

+ A
+ B
+ C

```
+ A
+ B
+ C
```


### 参考サイト
Markdown: 箇条書きリスト ul を作成する　　
https://step-learn.com/article/markdown/md-strong.html  


# 【1. 】番号付きリスト

1. 番号付きリスト_1
    1. 番号付きリスト_1_1
    1. 番号付きリスト_1_2
1. 番号付きリスト_2
1. 番号付きリスト_3


```
1. 番号付きリスト_1
    1. 番号付きリスト_1_1
    1. 番号付きリスト_1_2
1. 番号付きリスト_2
1. 番号付きリスト_3
```

### 参考サイト
Markdown: 箇条書きリスト ul を作成する　　
https://step-learn.com/article/markdown/md-strong.html  



# 目次 の作成
1. [内容1](#content1)
1. [内容2](#content2)
1. [内容3](#content3)

<a id="content1"></a>

# 内容1
詳細1

<a id="content2"></a>

# 内容2
詳細2

<a id="content3"></a>

# 内容3
詳細3


```
# 目次 の作成
1. [内容1](#content1)
1. [内容2](#content2)
1. [内容3](#content3)

<a id="content1"></a>

# 内容1
詳細1

<a id="content2"></a>

# 内容2
詳細2

<a id="content3"></a>

# 内容3
詳細3
```


### 参考サイト
Markdown で ページ内リンク付き の 目次 を 作成 する 方法  
https://qiita.com/miriwo/items/11b717dfc501b5b4e286#anchor1  



