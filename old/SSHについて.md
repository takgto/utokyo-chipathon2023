# sshとは
ネットワーク経由で他のコンピュータに接続してゴニョゴニョしたいときに使うものです。

## 繋げ方
```bash
ssh user名@ipアドレス
```
で繋げます。但し、ipアドレスは繋がるipアドレスであることが前提です。ここでは詳しく説明しません。

## ファイルをsshを利用してコピーする
基本的には[cpコマンド](https://github.com/yutyan0119/utokyo-chipathon2023/wiki/Linux%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E5%85%A5%E9%96%80#2-cp)とほぼ同じです。

```bash
# こちらから向こうにコピーする
scp file.txt user@192.168.1.1:/home/user/file.txt
# 向こうからこちらにコピーする
scp user@192.168.1.1:/home/user/file.txt file.txt
```

## X転送
向こう側でグラフィカルに表示されるべきものをこちらで見たいときにはX転送をします。接続時に`-X`コマンドを足します
```
ssh -X user名@ipアドレス
```
