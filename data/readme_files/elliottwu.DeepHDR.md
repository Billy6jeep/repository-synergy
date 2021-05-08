# ECCV'18: Deep High Dynamic Range Imaging with Large Foreground Motions
<img src="./img/hdr_teaser.jpg" width="800">

This is the implementation for [Deep High Dynamic Range Imaging with Large Foreground Motions](https://arxiv.org/abs/1711.08937), Shangzhe Wu, Jiarui Xu, Yu-Wing Tai, Chi-Keung Tang, in ECCV, 2018. More results can be found on our [project page](https://elliottwu.com/projects/hdr/). 

## Get Started
### Prerequisites
- Python 3.5
- [Tensorflow 1.4.0](https://github.com/tensorflow/tensorflow/tree/r1.4)
- OpenCV 3.4 (from [conda-forge](https://anaconda.org/conda-forge/opencv))
- [Photomatix](https://www.hdrsoft.com/) for tonemapping

### Setup
- Clone this repo: 
```bash
git clone https://github.com/elliottwu/DeepHDR.git
cd DeepHDR
```

- Download pretrained model: (~60MB)
```bash
sh download_pretrained.sh
```

### Demo
```bash
sh test.sh
```

### Tonemapping (post-processing)
Generated HDR images are in `.hdr` format, which may not be properly displayed in your image viewer directly. You may use [Photomatix](https://www.hdrsoft.com/) for tonemapping: 
- Download [Photomatix](https://www.hdrsoft.com/) free trial, which won't expire. 
- Load the generated `.hdr` file in Photomatix.
- Adjust the parameter settings. You may refer to pre-defined styles, such as `Detailed` and `Painterly2`. 
- Save your final image in `.tif` or `.jpg`. 

### Train
- Download Kalantari's dataset: (~8GB)
```bash
cd dataset
sh download_dataset.sh
cd ..
```
- Prepare [TFRecord](https://www.tensorflow.org/guide/datasets#consuming_tfrecord_data): (this takes ~10 minutes)
```bash
cd dataset
python convert_to_tfrecord.py
cd ..
```
- Start training: 
```bash
sh train.sh
```
- To monitor training using Tensorboard, copy the following to your terminal and open `localhost:8888` in your browser
```bash
tensorboard --logdir=logs --port=8888
```

### Citation
```
@InProceedings{Wu_2018_ECCV,
  author = {Wu, Shangzhe and Xu, Jiarui and Tai, Yu-Wing and Tang, Chi-Keung},
  title = {Deep High Dynamic Range Imaging with Large Foreground Motions},
  booktitle = {The European Conference on Computer Vision (ECCV)},
  month = {September},
  year = {2018}
}
```
