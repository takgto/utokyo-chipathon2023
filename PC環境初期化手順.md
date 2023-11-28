# PCセットアップ手順

前の人のデータなどが残っていて環境が汚れている場合に綺麗な環境をセットアップする方法を記します。

## 1. 新しいフォルダーを作る

```bash
cd
# この下のフォルダ名はなんでも良いです。
mkdir my_vitisai
```
## 2. Vitis-aiをクローンする
```bash
cd my_vitisai
git clone https://github.com/Xilinx/Vitis-AI -b 2.5 --depth 1
```
## 3. yolov3-dlabとedge-evalをクローンする
```bash
# my_vitisaiで実行する
git clone https://github.com/takgto/edge-eval
git clone https://github.com/takgto/yolov3-dlab
```
## 4. 学習済みweightをコピーする
**コピー元のパスは各個人に合わせること**
```bash
cp /mnt/c/Users/x-nics-kuroda/Downloads/work/yolov3-608_best_weights/yolov3-608_best.weights　/home/x-nics-kuroda/Vitis-AI/yolov3-dlab/work/backup
```
** 学習が終わらなかった場合には、Windowsの/Users/x-nics-kuroda/Downloads/work_best_weightsにあらかじめ用意されたyolov3-608_best.weghtsをコピーする **
```bash
cp /Users/x-nics-kuroda/Downloads/work_best_weights/yolov3-608_best_weights/yolov3-608_best.weights　/home/x-nics-kuroda/Vitis-AI/yolov3-dlab/work/backup
```
## 5. Docker起動
```bash
cd 
docker load -i vitis-ai-cpu.tar
cd my_vitisai
./docker_run.sh xilinx/vitis-ai-cpu:latest
```
## 6. Conda環境立ち上げ
```bash
conda activate vitis-ai-tensorflow2
pip install dm-tree~=0.1.1
pip install tensorflow==2.8.0
cd /workspace/src/Vitis-AI-Quantizer/vai_q_tensorflow2.x/pkgs
pip install --force-reinstall *.whl
pip install keras_applications 
```
### pkgsディレクトリがないと言われた場合
以下をDocker内で実行すればok
```bash
cd ~/Vitis-AI/src/Vitis-AI-Quantizer/vai_q_tensorflow2.x
export SRC_DIR=$(pwd)
cd /workspace/src/Vitis-AI-Quantizer/vai_q_tensorflow2.x 
sh vai_q_tensorflow2_cpu_feedstock/build.sh 
```
## 7.darknet2keras
```bash
cd /workspace/yolov3-dlab/scripts_tf2
./convert_yolov3.sh
# /workspace/yolov3-dlab/keras_modelにファイルが生成されるはずです
```
## 8. quantize keras model
```bash
cd /workspace/yolov3-dlab/scripts_tf2
python my_quantizer.py -i
```

## 9. compile model for fpga
```bash
cd /workspace/yolov3-dlab/scripts_tf2/compile_yolov3.sh
```
