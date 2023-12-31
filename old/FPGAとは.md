# FPGAとは

FPGAとは、Field Programmable Gate Arrayの略であり、簡単に言うとプログラム可能回路です。LUT(Look Up Table)やFF(Flip Flop)などで構成されていて、それらが書き換わることで書き換え可能な回路を実現しています。FPGAは汎用プロセッサやソフトウェアと比べて高速、低電力で動作することで知られており、現在主に組み込み等の様々な場面で使用されています。例えば、今回作成する物体認識アプリケーションも車載での使用を意識したものです。

# FPGA上のアプリケーションの開発

FPGA上のアプリケーション開発は通常、VerilogやVHDL等のHDL(Hardware Description Language)を用いて開発されます。HDLはデジタル回路をプログラミング言語のように記述できる言語ですが、その構造はプログラミング言語とは異なっており、慣れてないうちは難しいかもしれません。今回用いるFPGAは特殊な構造をしているのでHDLを用いずにPythonやC++で開発することも可能ですが、HDLを用いるとより高性能なハードウェアの作成も可能なので、興味がある人は是非調べてみてください。

# 今回用いるFPGA

今回用いるFPGAは[Kria KV260 Vision AI Starter Kit](https://japan.xilinx.com/products/som/kria/kv260-vision-starter-kit.html)というものですが、このFPGAは通常のFPGAに比べて特殊な構造になっています。具体的には、FPGA上にLinuxが動作するプロセッサ(PS)が載っていて、ソフトウェアプログラムが動作します。通常のFPGAの部分はPLと呼ばれ、PS上のプログラムからAXIというインターフェースを用いてPL上で作成した回路にアクセスをすることが出来ます。つまり、基本的な処理の流れはPSでプログラムとして行い、特定の処理をPL上の回路で高速化するというのが今回の開発の流れになります。実際、みなさんが用いるVitisAIも、AIの処理部分をDPUという回路で高速化しています。

# 開発フロー

基本的にはVitisAIを用いて資料のとおりに開発をしていただきますので、詳しいことは資料を参照してください。簡単にまとめると、
- データセットを用いて、学習をする
- 学習したモデルを量子化する
- kv260向けに量子化したモデルをコンパイルする
- コンパイル済モデル、実行プログラムをFOGA上に転送し、FPGA上で推論を実行する

という流れになります。 また、HDLを用いて開発をすることも出来ます。その場合は、[kv260向けプラットフォーム作成方法](https://github.com/yutyan0119/utokyo-chipathon2023/wiki/kv260%E5%90%91%E3%81%91%E3%83%97%E3%83%A9%E3%83%83%E3%83%88%E3%83%95%E3%82%A9%E3%83%BC%E3%83%A0%E3%81%AE%E4%BD%9C%E6%88%90%E6%96%B9%E6%B3%95)を参考にするか、TAにご相談ください。

FPGAの基礎的な知識については、[東大電気系のCPU実験のwiki](https://exp.mtl.t.u-tokyo.ac.jp/2022/b3exp/-/wikis/aboutFPGA)が詳しいので、ぜひそちらも参考にしてみてください。