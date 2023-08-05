FPGAの環境をリセットしたい時にやることです。

**注意：FPGAの環境が完全に綺麗さっぱりになってしまいます。保存しておきたデータは予めPCに移しておきましょう**

**わからなければTA/先生を呼んでください！**

## 1. SDカードにOSを焼く
**ここでSDカードにOSをクリーンインストールしてしまうとFPGAの作業は元に戻せません。自分が編集したコードや、prototxtなど、保存しておきたいものはPCに移動しておいてください！！！**

もしマイクロSDカードをPCに刺すアダプタが無ければTAか先生に言ってください。（講義で使用するPCはSDカードソケットがあるので、SDカード型にして刺すことが出来ます）

1. DownloadsフォルダにあるbalenaEtcherを起動
2. balenaEtherのFlash from fileで、Downloadsフォルダにある`petalinux-sdimage-2021.1-update1.wc.xz`を選択
3. Select targetでMicroSDカードを選択
4. Flash!を選択

## 2. FPGA起動
いつもどおり、MicroSDを指してFPGAを起動してください。MobaXTermでFPGAがしっかり起動すればOKです。
以下を入力してください。

```bash
ifconfig eth0 192.168.1.100 netmask 255.255.255.0 up
```
これで`ifconfig`したときに、ipアドレスが192.168.1.100になっていればOKです。

## 3. FPGAの環境構築
以下を実行してください。
```bash
cd Vitis-AI/edge-eval
sshpass -p "root" scp init260.sh root@192.168.1.100:/home/root
sshpass -p "root" scp aliases root@192.168.1.100:/home/root
sshpass -p "root" scp -r data root@192.168.1.100:/home/root
sshpass -p "root" scp cpp/* root@192.168.1.100:/home/root/Vitis-AI/examples/Vitis-AI-Library/samples/yolov3
sshpass -p "root" scp -r video root@192.168.1.100:/home/root/Vitis-AI/examples/Vitis-AI-Library/samples/yolov3
sshpass -p "root" scp -r mAP root@192.168.1.100:/home/root/Vitis-AI/examples/Vitis-AI-Library/samples/yolov3
sshpass -p "root" scp -r dpu_yolov3 root@192.168.1.100:/usr/share/vitis_ai_library/models
```

あとはいつもどおりの手順です。