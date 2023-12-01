# Dockerについて
Dockerについて詳しいことを説明すると本になるので、ここでは詳しくは取り上げません。
オススメ記事は『[実践 Docker - ソフトウェアエンジニアの「Docker よくわからない」を終わりにする本](https://zenn.dev/suzuki_hoge/books/2022-03-docker-practice-8ae36c33424b59)』です。

Dockerとは、ようするに皆さんの使用しているコンピュータ上で綺麗な環境を仮想的に実現するためのツールです。内部的にはcgroupなどが使用されていますが、ここでは割愛します。

# Dockerの大体を掴む
1. ある環境を使用したいとする
2. その環境を構築するようなDockerfileを作成する
3. それをbuildしてimageを作る（このimageはOSファイルのようなもの）
4. そのimageからcontainerを作る

これだけです。講義で行われている`docker load -i vitis-ai-cpu.tar`は、ビルドされたimageのファイルをdockerに読み込ませて、imageとしてロードしています。
`./docker_run.sh xilinx/vitis-ai-cpu:latest` は、`xilinx/vitis-ai-cpu:latest`というイメージを使用して、コンテナを立ち上げています。

詳しいことは`./docker_run.sh`の中身を見ましょう。