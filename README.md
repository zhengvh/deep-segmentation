# Deep Segmentation

This repository contains several CNNs for semantic segmentation (U-Net, SegNet, ResNet, FractalNet) using Keras library.
The code was developed assuming the use of depth data (e.g. Kinect, Asus Xtion Pro Live).

This project has been included in the paper "Convolutional Networks for Semantic Heads Segmentation using Top-View Depth Data in Crowded Environment" accepted in Internation Conference on Pattern Recognition (ICPR), 2018.
Tested on:

* Ubuntu 16.04
* Python 3.5.2
* Keras 2.2.2
* TensorFlow 1.7.0

You can test these scripts on the following datasets:

* [TVHeads (Top-View Heads) Dataset](http://vrai.dii.univpm.it/tvheads-dataset)
* [PIDS (Preterm Infants' Depth Silhouette) Dataset](http://vrai.dii.univpm.it/pids-dataset)

[![YouTubeDemoHeads](https://img.youtube.com/vi/MWjcW-3A5-I/0.jpg)](https://www.youtube.com/watch?v=MWjcW-3A5-I)
[![YouTubeDemoInfant](https://img.youtube.com/vi/_GCnkUXPTJk/0.jpg)](https://www.youtube.com/watch?v=_GCnkUXPTJk)

## Data
Provided data is processed by `data.py` script. This script just loads the images and saves them into NumPy binary format files `.npy` for faster loading later.

```bash
python data.py
```
## Models
The provided models are basically a convolutional auto-encoders.
```
python train_fractal_unet.py
python train_resnet.py
python train_segnet.py
python train_unet.py
python train_unet2.py
python train_unet3_conv.py
```
These deep neural network is implemented with Keras functional API.

Output from the networks is a 96 x 128 which represents mask that should be learned. Sigmoid activation function makes sure that mask pixels are in [0, 1] range.

## Prediction

You can test the online prediction with an OpenNI registration (`.oni` file).
```
python online_prediction.py --v <oni_video_path>
```
Requirement for this is OpenNI2 installation: https://github.com/occipital/OpenNI2, then link the libOpenNI2.so and the OpenNI2 directory in the script path. Before launching the script create a folder ```predicted_images```.

### Python Environment Setup

```bash
sudo apt-get install python3-pip python3-dev python-virtualenv # for Python 3.n
virtualenv -p python3 deepseg
. deepseg/bin/activate
```

The preceding command should change your prompt to the following:

```
(deepseg)$ 
```
Install TensorFlow in the active virtualenv environment:

```bash
pip3 install --upgrade tensorflow-gpu # for Python 3.n and GPU
```

Install the others library:

```bash
pip3 install --upgrade keras scikit-learn scikit-image h5py opencv-python primesense
```
### Run

* Create a folder `raw` in the same filesystem level of the above python scripts.
* Download the dataset and extract all the images in a folder `raw`/`train`.
* Run `python data.py` a folder `npy` will be created containig Numpy binary format npy files with traning and validation dataset.
* Run the above python training and testing scripts, for example `python train_unet3_conv.py`.
* Log files with final results `log_conv_8.csv` and `log_conv_16.csv` will be created.
* Predicted images for the test data will be stored in folders `preds_16` and `preds_8`.

### Authors
* Daniele Liciotti | [GitHub](https://github.com/danielelic)
* Rocco Pietrini | [GitHub](https://github.com/roccopietrini)

### Acknowledgements
* This work is partially inspired by the work of [jocicmarko](https://github.com/jocicmarko).
