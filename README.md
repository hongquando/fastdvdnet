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
pip3 install -r /content/fastdvdnet/requirements.txt
pip3 install --extra-index-url https://developer.download.nvidia.com/compute/redist/cuda/10.0 nvidia-dali==0.10.0
```
### Testing

If you want to denoise an image sequence using the pretrained model you can execute

```
python3 test_fastdvdnet.py \
	--test_path ./test/ \
	--noise_sigma 30 \
	--model_file /content/fastdvdnet/logs/net.pth \
	--save_path ./results/
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
	--repeat_data 10 \
	--noise_ival 5 55 \
	--val_noiseL 25 \
	--log_dir logs \
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


