# Git 101

> date: 2017.06.04
>
> author: R1x
>
> version: 0.1.0

### 什麼是Git??

* Git是一個分佈式版本控制軟體

### 什麼是版本控制??

* 版本控制就是一種為了要將檔案的修改過程進行紀錄, 所使用的手段.

* 這就也算一種版本控制

```
drwxr-xr-x   8 rex  staff   272 Jun  3 23:06 .
drwx------+ 14 rex  staff   476 Jun  3 22:56 ..
-rw-r--r--@  1 rex  staff  8196 Jun  3 22:56 .DS_Store
drwxr-xr-x   3 rex  staff   102 Jun  3 22:54 第一次用git就上手
drwxr-xr-x   4 rex  staff   136 Jun  3 22:55 第一次用git就上手_01
drwxr-xr-x   4 rex  staff   136 Jun  3 22:55 第一次用git就上手_02
drwxr-xr-x   4 rex  staff   136 Jun  3 22:55 第一次用git就上手_03
drwxr-xr-x   4 rex  staff   136 Jun  3 22:55 第一次用git就上手_04
```

### 要把檔案恢復到編輯前的狀態，能怎麼做??

* 除了通靈之外, 最直接的方式就是平時養成習慣複製多個檔案，用檔名來區分日期和版本。

* 一但遇到問題必須得回朔到過去的狀態，就只能透過檔案名稱判斷時間點進行復原的動作.

* 然而在團隊合作的專案中, 若是沒溝通好, 除了隊友要一直問<del>候</del>之外, 更徒增了許多維護、查詢與交接的困難.

### 為什麼要用Git??
*  <del>減少通靈的頻率。</del>
*  <del>減少問候的次數。</del> 
*  更有系統的管理檔案。

### 怎麼用??
1. 直接在黑黑的視窗(Command Line)敲指令
2. 用別人做好的GUI管理介面
3. 直接在GitHub的網頁直接操作

### 基本流程

|名稱         | 用途           | 指令 |
|--------------------|------------------|-----------------------|
|1.建立/切換 專案目錄  | ... | mkdir "project name" <br> cd "project name" |
|2. 同步資料      | 複製專案 or 下載分支 | git clone "https://github.com/Jericho229/study_note" <br> "git pull https://github.com/Jericho229/study_note"   |
|3. 切換分支 branch  | 切換到自己的分支    | git checkout -b "your branch name" |
|4. ---編輯A.html---    | coding ||
|4. ---編輯B.css---    | coding ||
|4. ---編輯C.js---    | coding ||
|5. 檢視狀態  | 查看檔案目錄目前的狀態    | git stauts |
|6. 新增檔案  | 將修改的檔案加入編輯名單    | git add "single file" (加入單檔) <br> git add . (全部加進去) |
|7. 編輯異動描述 | 簡單敘述你新增/修改了什麼    | git commit -m "change log" |
|8. 提交檔案 | 將修改的內容送上伺服器    | git push origin "remote branch"|
|9. ---再次編輯A.html---    | 繼續coding <br> 重複步驟5~8 ||


### 初次設定

1. 建立ssh key (可略過）

2. 設定config

```
$ git config user.name "Your Name"

$ git config user.email "yourmail@mail.com"
```

## 常用指令

### Git 複製專案

```
git clone git@github.com:Jericho229/study_note.git
```

### Git 更新內容
```
git pull origin
```
* origin: 來源目的地


### Git 查看檔案狀態 

```
git stauts 
```

### Git Branch管理
```
git branch ## 列出(local端）所有分支
git branch -m "name" # 更改名稱
```

### Git Branch切換

```
git checkout "other branch" # 切換到該分支
git checkout -b "other branch" # 新增並切換到該分支
```

### 更新分支目錄
```
git fetch origin
```
* origin: 來源目的地

### Git 比較修改內容 

```
git diff < file > #比較當前文件和暫存區文件差異
git diff 
```

### Git 新增檔案

先將修改的檔案列入暫存, 作為commit使用

```
git add . (將所有修改列入暫存)
git add filename (對單檔)
```

### Git Commit

```
git commit
git commit -m 'commit message'
git commit -a -m 'commit -message' # 將所有修改過得檔案都 commit, 但是 新增的檔案 還是得要先 add.
```

### Git提交檔案
```
git push origin
```
* origin: 提交目的地

### Git 刪除檔案

```
git rm "filename"
```


### Git 分支合併

將branch分支合併到當前分支

```
git merge "branch name" 

```

### Git 回朔

```
git reset < file > #將單檔從暫存區恢復到工作文件
git reset -- . #從暫存區恢復到工作文件
```

### Git 檢查設定

$ git config --list

```
	user.name=Jimmy Kuo
	user.email=jimmy@gogojimmy.net
```

-

### Git 遠程倉庫管理
```
git remote - v #查看遠 ​​程服務器地址和倉庫名稱
git remote show origin #查看遠 ​​程服務器倉庫狀態
git remote add origin git@github : XXX / test . git #添加遠程倉庫地址
git remote set - url origin git@github . com : XXX / test . git #設置遠程倉庫地址(用於修改遠程倉庫地址)
```

### 唐鳳表示：
當年怎麼記住Git指令呢？是這樣的：

1. 在碰到新的事情的時侯，要先Fetch新的狀況（接受它）。
2. 接下來要跟自己心裡的想法Merge（面對它）。這時可能產生衝突，衝突是要解決的。
3. 衝突解決之後才能夠採取行動，所以要Commit（處理它）。
4. 最後再Push（放下它）。
	* 為什麼是放下它呢？因為你一旦把Code push出去、開源之後，它就不是你的了。




