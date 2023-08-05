最低限これだけは覚えてほしいコマンド達です。
# Lnuxコマンド
## 1. cd
意味：指定したディレクトリに移動する

使い方
```bash
cd /path/to/dir
```
## 2. cp
意味：指定したファイルやディレクトリを指定した場所にコピーする

使い方
```bash
cp file.txt test/file.txt
# 同じ意味
cp file.txt test/
# ファイル名を変える時
cp file.txt test/file2.txt
# ディレクトリごとコピーするとき
cp -r test test2
```

## 3. mv
意味：指定したファイルやディレクトリを指定した場所に移動する

使い方
```bash
mv file.txt test/file.txt
# 名前を変えたいときにも使える
mv file.txt filefile.txt
```

## 4. touch
意味：ファイルを作成する（既にあるときは上書きしない）（本来の意味とは違いますが、これでほぼ問題ないです）

使い方
```bash
touch test.txt
```

## 5. ls
意味：指定したディレクトリにあるファイルを閲覧する

使い方
```bash
ls # 今のディレクトリのファイルが見える
ls test/ # testディレクトリのファイルが見える
ls -a # 隠しファイルも含めて見る
ls -lah # 容量とかも見る
```

## 6. mkdir
意味：ディレクトリを作る

使い方
```bash
mkdir test
```