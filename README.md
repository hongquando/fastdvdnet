# FastDVDnet

## Architecture

<img src="https://github.com/m-tassano/fastdvdnet/raw/master/img/arch.png" heigth=350>

## Code User Guide

### Dependencies

The code runs on Python +3.6. You can create a conda environment with all the dependecies by running
```
conda env create -f requirements.yml -n <env_name>
```
NOTE: the code was updated to support a newer version of the DALI library. For the original version of the algorithm which supported pytorch=1.0.0 and nvidia-dali==0.10.0 you can see this [release](https://github.com/m-tassano/fastdvdnet/releases/tag/v0.1)
```
pip3 install -r requirements.txt
```
### Testing

If you want to denoise an image sequence using the pretrained model you can execute

```
python3 test_fastdvdnet.py \
	--test_path ./test/ \
	--noise_sigma 30 \
	--model_file ./logs/net.pth \
	--save_path ./results/
	--crop
```

**NOTES**
* The image 3D should be stored under <path_to_input_sequence>
* The model has been trained for values of noise in [5, 55]
* run with *--no_gpu* to run on CPU instead of GPU
* run with *--save_noisy* to save noisy frames
* run with *--help* to see details on all input parameters

### Training

If you want to train your own models you can execute

```
python3 train_fastdvdnet.py \
	--trainset_dir ./train \
	--valset_dir ./valid \
	--epoch 80 \
	--repeat_data 25 \
	--noise_ival 5 55 \
	--val_noiseL 25 \
	--batch_size 64 \
	--log_dir logs \
	--crop
```

**NOTES**
* As the dataloader in based on the DALI library, the training image must be provided as .mat files, all under <path_to_input_mat>
* The validation sequences must be stored as image 3D in individual folders under <path_to_val_sequences>
* run with *--help* to see details on all input parameters

### Resume training

```
python3 train_fastdvdnet.py \
	--trainset_dir ./train \
	--valset_dir ./valid \
	--log_dir logs \
	--epoch 120 \
	--resume_training
```

### ABOUT
Copying and distribution of this file, with or without modification, are permitted in any medium without royalty provided the copyright notice and this notice are preserved. This file is offered as-is, without any warranty.

- Author : Matias Tassano ```mtassano at gopro dot com```
- Copyright : (C) 2019 Matias Tassano
- Licence : GPL v3+, see GPLv3.txt

The sequences are Copyright GoPro 2018

